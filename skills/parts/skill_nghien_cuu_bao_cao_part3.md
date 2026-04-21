# Phần 3/4: Generator Script - Setup & Helper Functions
> 💡 **Chú ý cho AI:** Đây là phần 3 của Skill Báo Cáo. Bạn cần đọc 4 phần để hoạt động chính xác.

## 7. Trình Tạo DOCX Bằng Python — CHUẨN Format MauDATN_2021

> 🔑 **ĐÂY LÀ OUTPUT CUỐI CÙNG.** Khi user yêu cầu file docx, PHẢI cung cấp đoạn code này đã được điền nội dung thực tế từ dự án.

```python
# -*- coding: utf-8 -*-
"""
Tạo Báo Cáo Đồ Án/Luận Văn TDTU — Chuẩn MauDATN_2021
Font: Times New Roman 13pt | Lề: 3.5/3.0/3.5/2.0 cm | 1.5 line spacing
"""
from docx import Document
from docx.shared import Pt, Cm, Inches, Emu
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.oxml.ns import qn
from docx.oxml import OxmlElement
from docx.shared import RGBColor
import os, subprocess, tempfile

# ============================================================
# HẰNG SỐ KÍCH THƯỚC TRANG TDTU (MauDATN_2021)
# Chỉnh ảnh sẽ căn cứ vào 2 giá trị này để luôn vừa trang
# ============================================================
TDTU_MAX_W_CM = 15.5   # Usable width  = 21.0 - 3.5 - 2.0
TDTU_MAX_H_CM = 12.0   # Max height for 1 diagram (half-page, đẹp mắt)
TDTU_FULL_H_CM = 20.0  # Max height khi biểu đồ chiếm gần hết trang

def setup_styles(doc):
    """Cài đặt tất cả styles chuẩn TDTU từ MauDATN_2021."""
    
    # --- Normal Style (Nội dung chính) ---
    style_normal = doc.styles['Normal']
    style_normal.font.name = 'Times New Roman'
    style_normal.font.size = Pt(13)
    style_normal.paragraph_format.line_spacing = 1.5
    style_normal.paragraph_format.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
    style_normal.paragraph_format.space_before = Pt(0)
    style_normal.paragraph_format.space_after = Pt(6)
    # Fix font cho tiếng Việt
    style_normal.element.rPr.rFonts.set(qn('w:eastAsia'), 'Times New Roman')
    
    # --- Heading 1 (Chương: IN HOA, Bold, 14pt, Căn giữa) ---
    h1 = doc.styles['Heading 1']
    h1.font.name = 'Times New Roman'
    h1.font.size = Pt(14)
    h1.font.bold = True
    h1.font.color.rgb = RGBColor(0, 0, 0)
    h1.paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER
    h1.paragraph_format.space_before = Pt(12)
    h1.paragraph_format.space_after = Pt(6)
    h1.paragraph_format.page_break_before = True  # Luôn ngắt sang trang mới khi bắt đầu Chương
    
    # --- Heading 2 (Mục 1.x: Bold, 13pt) ---
    h2 = doc.styles['Heading 2']
    h2.font.name = 'Times New Roman'
    h2.font.size = Pt(13)
    h2.font.bold = True
    h2.font.color.rgb = RGBColor(0, 0, 0)
    h2.paragraph_format.alignment = WD_ALIGN_PARAGRAPH.LEFT
    h2.paragraph_format.space_before = Pt(6)
    h2.paragraph_format.space_after = Pt(3)
    
    # --- Heading 3 (Mục 1.x.x: Bold Italic, 13pt) ---
    h3 = doc.styles['Heading 3']
    h3.font.name = 'Times New Roman'
    h3.font.size = Pt(13)
    h3.font.bold = True
    h3.font.italic = True
    h3.font.color.rgb = RGBColor(0, 0, 0)
    h3.paragraph_format.alignment = WD_ALIGN_PARAGRAPH.LEFT


def add_toc(doc, title='MỤC LỤC'):
    """
    Chèn Mục Lục tự động vào Word (TOC Field).
    Sau khi mở file .docx, nhấn F9 (hoặc click Update Table)
    để Word tự điền số trang dựa trên Heading 1/2/3.
    """
    # Tiêu đề MỤC LỤC
    p_title = doc.add_paragraph(title)
    p_title.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p_title.runs[0]
    run.font.name = 'Times New Roman'
    run.font.size = Pt(16)
    run.font.bold = True

    # Đoạn chứa TOC field
    paragraph = doc.add_paragraph()
    run = paragraph.add_run()

    # begin field
    fldChar_begin = OxmlElement('w:fldChar')
    fldChar_begin.set(qn('w:fldCharType'), 'begin')
    fldChar_begin.set(qn('w:dirty'), 'true')   # Đánh dấu cần update
    run._r.append(fldChar_begin)

    # instruction: TOC \o "1-3" \h \z \u
    # \o 1-3  = lấy Heading 1 đến Heading 3
    # \h      = hyperlink (click tên mục → nhảy tới trang)
    # \z      = ẩn số trang khi ở Web view
    # \u      = dùng paragraph outline level
    instrText = OxmlElement('w:instrText')
    instrText.set(qn('xml:space'), 'preserve')
    instrText.text = ' TOC \\o "1-3" \\h \\z \\u '
    run._r.append(instrText)

    # separate (placeholder khi chưa update)
    fldChar_sep = OxmlElement('w:fldChar')
    fldChar_sep.set(qn('w:fldCharType'), 'separate')
    run._r.append(fldChar_sep)

    # Dòng placeholder báo user cần nhấn F9
    placeholder = OxmlElement('w:r')
    placeholder_text = OxmlElement('w:t')
    placeholder_text.text = '[Nhấn Ctrl+A rồi F9 để cập nhật Mục Lục]'
    placeholder.append(placeholder_text)
    run._r.append(placeholder)

    # end field
    fldChar_end = OxmlElement('w:fldChar')
    fldChar_end.set(qn('w:fldCharType'), 'end')
    run._r.append(fldChar_end)


def add_image_fitted(doc, img_path,
                     max_width_cm=TDTU_MAX_W_CM,
                     max_height_cm=TDTU_MAX_H_CM):
    """
    Chèn ảnh vào Word với kích thước tự động vừa trang TDTU.
    
    Logic:
      - Giữ tỷ lệ (ảnh không bị méo)
      - Chiều rộng tối đa = 15.5 cm (vừa với lề TDTU)
      - Chiều cao tối đa = 12 cm (mặc định) hoặc 20 cm (full-page)
      - Tự động co nhỏ cạnh vượt giới hạn
      - Ảnh được căn giữa trang (Centered)
    """
    try:
        from PIL import Image
        img = Image.open(img_path)
        img_w_px, img_h_px = img.size
        # DPI mặc định khi xuất ảnh (mmdc/kroki thường 300 DPI)
        dpi = img.info.get('dpi', (150, 150))[0] or 150
        img_w_cm = (img_w_px / dpi) * 2.54
        img_h_cm = (img_h_px / dpi) * 2.54
    except ImportError:
        # Fallback: không có Pillow, đặt chiều rộng cố định bằng max
        img_w_cm, img_h_cm = max_width_cm, max_height_cm

    # Tính tỷ lệ scale
    scale = 1.0
    if img_w_cm > max_width_cm:
        scale = max_width_cm / img_w_cm
    if img_h_cm * scale > max_height_cm:
        scale = min(scale, max_height_cm / img_h_cm)

    final_w = Cm(img_w_cm * scale)
    final_h = Cm(img_h_cm * scale)

    # Chèn ảnh vào đoạn căn giữa
    p = doc.add_paragraph()
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    p.paragraph_format.keep_with_next = True  # Giữ ảnh và caption luôn dính liền nhau, không bị tách trang
    run = p.add_run()
    run.add_picture(img_path, width=final_w, height=final_h)
    return final_w, final_h


def render_mermaid_to_png(mermaid_code: str,
                          output_png: str = None,
                          width_px: int = 1800,
                          bg_color: str = 'white') -> str:
    """
    Render Mermaid code → PNG rồi chèn vào Word.
    
    ưu tiên:
      1. Dùng `mmdc` (mermaid-cli) nếu đã cài:  npm install -g @mermaid-js/mermaid-cli
      2. Fallback: Gọi API kroki.io (không cần cài đặt gì, cần Internet)
    
    Tham số width_px: 1800px @ 150dpi ≈ 30cm (sẽ bị scale xuống 15.5cm bởi add_image_fitted)
    → chữ vẫn to, rõ ràng sau khi thu nhỏ
    """
    if output_png is None:
        output_png = os.path.join(tempfile.gettempdir(), 'mermaid_diagram.png')

    # --- Cách 1: mmdc (mermaid-cli) ---
    mmd_file = output_png.replace('.png', '.mmd')
    with open(mmd_file, 'w', encoding='utf-8') as f:
        f.write(mermaid_code)

    try:
        result = subprocess.run(
            ['mmdc', '-i', mmd_file, '-o', output_png,
             '-w', str(width_px), '-b', bg_color,
             '--scale', '2'],   # Retina 2x → chữ rõ hơn
            capture_output=True, timeout=30
        )
        if result.returncode == 0 and os.path.exists(output_png):
            print(f'[OK] Mermaid -> {output_png} (via mmdc)')
            return output_png
    except (FileNotFoundError, subprocess.TimeoutExpired):
        pass

    # --- Cách 2: kroki.io API (fallback) ---
    try:
        import requests, base64, zlib
        compressed = zlib.compress(mermaid_code.encode('utf-8'), 9)
        encoded = base64.urlsafe_b64encode(compressed).decode('ascii')
        url = f'https://kroki.io/mermaid/png/{encoded}'
        resp = requests.get(url, timeout=15)
        if resp.status_code == 200:
            with open(output_png, 'wb') as f:
                f.write(resp.content)
            print(f'[OK] Mermaid -> {output_png} (via kroki.io)')
            return output_png
    except Exception as e:
        print(f'[WARN] kroki.io thất bại: {e}')

    print('[ERROR] Không render được Mermaid. Cài mmdc: npm install -g @mermaid-js/mermaid-cli')
    return None


def add_mermaid_to_doc(doc, mermaid_code: str,
                       fig_number: str, caption: str,
                       full_page: bool = False):
    """
    Hàm tiện ích: Render Mermaid + chèn vào Word đúng kích thước TDTU.
    
    full_page=True  → cho phép biểu đồ cao tới 20cm (gần hết trang)
    full_page=False → giới hạn 12cm (biểu đồ nằm giữa trang, vừa mắt)
    """
    max_h = TDTU_FULL_H_CM if full_page else TDTU_MAX_H_CM
    png_path = render_mermaid_to_png(mermaid_code)
    if png_path:
        add_image_fitted(doc, png_path,
                        max_width_cm=TDTU_MAX_W_CM,
                        max_height_cm=max_h)
        add_figure_caption(doc, fig_number, caption)
    else:
        # Fallback: dán Mermaid code dưới dạng text nếu không render được
        doc.add_paragraph(f'[Biểu đồ Mermaid — {caption}]\n{mermaid_code[:300]}...')
        add_figure_caption(doc, fig_number, caption)


def add_figure_caption(doc, fig_number, caption_text):
    """Thêm chú thích hình bên dưới — 12pt, Italic, Căn giữa."""
    p = doc.add_paragraph(f'Hình {fig_number}: {caption_text}')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]
    run.font.name = 'Times New Roman'
    run.font.size = Pt(12)
    run.font.italic = True


def add_table_caption(doc, table_number, caption_text):
    """Thêm chú thích bảng bên trên — 12pt, Italic, Căn giữa."""
    p = doc.add_paragraph(f'Bảng {table_number}: {caption_text}')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    p.paragraph_format.keep_with_next = True  # Nhằm giữ caption luôn đi kèm với bảng ở trang dưới
    run = p.runs[0]
    run.font.name = 'Times New Roman'
    run.font.size = Pt(12)
    run.font.italic = True


def render_latex_to_png(latex_str: str, eq_number: str = '',
                        output_path: str = None, fontsize: int = 16) -> str:
    """
    Render công thức LaTeX → PNG dùng matplotlib mathtext.

    Quy tắc KÍch THƯỚC đồng đều:
      - Tất cả công thức dùng fontsize=16 (trừ siêu phức tạp dùng 14)
      - Figure width cố định = 6.1 inch (= 15.5 cm, vừa vặn trang TDTU)
      - Height tự động co theo chiều đứng của công thức (tight_layout)
      - DPI = 200 → khi thu nhỏ vào DOCX chữ vẫn sắc nét
      - Nền trắng, không có trục/viền thừa

    Cú pháp LaTeX hay dùng trong báo cáo kỹ thuật:
      r'$v = \\omega \\cdot r$'                 # vận tốc bánh xe
      r'$PID = K_p e + K_i\\int e\\,dt + K_d\\dot{e}$'
      r'$P = U \\cdot I$'
      r'$T = \\frac{1}{f}$'
      r'$\\theta = \\arctan\\!\\left(\\frac{y}{x}\\right)$'
      r'$\\Delta\\phi = \\frac{\\Delta s_R - \\Delta s_L}{L}$'  # differential drive
    """
    if output_path is None:
        output_path = os.path.join(tempfile.gettempdir(), f'eq_{hash(latex_str)}.png')

    import matplotlib
    matplotlib.use('Agg')
    import matplotlib.pyplot as plt

    # Đảm bảo chuỗi được bao ngoài bởi $...$
    if not latex_str.strip().startswith('$'):
        latex_str = f'${latex_str.strip()}$'

    fig = plt.figure(figsize=(6.1, 0.8))  # width cố định, height sẽ tự co
    fig.patch.set_facecolor('white')
    ax = fig.add_axes([0, 0, 1, 1])
    ax.set_axis_off()
    ax.set_facecolor('white')

    # Đánh số công thức bên phải nếu có eq_number
    full_text = latex_str
    if eq_number:
        full_text = latex_str  # công thức ở giữa
        ax.text(0.98, 0.5, f'({eq_number})',
                transform=ax.transAxes,
                fontsize=fontsize - 2,
                va='center', ha='right',
                fontfamily='serif')

    ax.text(0.5, 0.5, full_text,
            transform=ax.transAxes,
            fontsize=fontsize,
            va='center', ha='center',
            fontfamily='serif')

    plt.savefig(output_path, dpi=200, bbox_inches='tight',
                facecolor='white', pad_inches=0.1)
    plt.close(fig)
    return output_path


def add_equation(doc, latex_str: str, eq_number: str = '',
                 label: str = '', fontsize: int = 16):
    """
    Chèn công thức toán học vào Word.

    Ưu tiên:
      1. Native Word Equation (OMML) — click được, sửa được trong Word
         Dùng khi latex đơn giản (không có \\int, \\sum phức tạp lồng nhau)
      2. Fallback → PNG (render bằng matplotlib mathtext)
         Dùng cho công thức phức tạp, đẹp hơn khi in

    Định dạng:
      - Căn giữa trang
      - Cùng fontsize cho tất cả công thức (mặc định 16pt)
      - Số công thức dạng (3.1) ở cột phải
      - Mô tả (label) in nghiêng bên dưới nếu có

    Ví dụ dùng:
      add_equation(doc, r'$v = \\omega \\cdot r$', '3.1', 'Vận tốc tuyến tính bánh xe')
      add_equation(doc, r'$PID = K_p e + K_i\\int e\\,dt$', '3.2', 'Bộ điều khiển PID')
    """
    try:
        # Thử chèn OMML native equation
        # Chuyển $..$ → plain LaTeX để xử lý
        plain = latex_str.strip().lstrip('$').rstrip('$').strip()

        # Tạo đoạn văn chứa equation
        p = doc.add_paragraph()
        p.alignment = WD_ALIGN_PARAGRAPH.CENTER

        from docx.oxml.ns import nsmap
        # OMML namespace
        OMML_NS = 'http://schemas.openxmlformats.org/officeDocument/2006/math'
        oMath = OxmlElement('{%s}oMath' % OMML_NS)

        # Chèn run chứa LaTeX text (Word sẽ hiển thị gần đúng)
        r = OxmlElement('{%s}r' % OMML_NS)
        rPr = OxmlElement('{%s}rPr' % OMML_NS)
        sty = OxmlElement('{%s}sty' % OMML_NS)
        sty.set('{%s}val' % OMML_NS, 'i')  # italic
        rPr.append(sty)
        r.append(rPr)
        t_elem = OxmlElement('{%s}t' % OMML_NS)
        t_elem.text = plain
        r.append(t_elem)
        oMath.append(r)

        p._p.append(oMath)

        # Thêm số công thức bên phải
        if eq_number:
            run_num = p.add_run(f'\t\t\t({eq_number})')
            run_num.font.name = 'Times New Roman'
            run_num.font.size = Pt(13)

    except Exception:
        # Fallback: render PNG
        png = render_latex_to_png(latex_str, eq_number=eq_number, fontsize=fontsize)
        add_image_fitted(doc, png, max_width_cm=TDTU_MAX_W_CM, max_height_cm=3.5)

    # Mô tả bên dưới (nếu có)
    if label:
        p_label = doc.add_paragraph(f'trong đó: {label}')
        p_label.paragraph_format.left_indent = Cm(1.5)
        run_lbl = p_label.runs[0]
        run_lbl.font.name = 'Times New Roman'
        run_lbl.font.size = Pt(13)
        run_lbl.font.italic = True


def _add_page_field(run, fmt='PAGE'):
    """Helper: chèn field PAGE hoặc NUMPAGES vào run."""
    fldChar = OxmlElement('w:fldChar')
    fldChar.set(qn('w:fldCharType'), 'begin')
    instrText = OxmlElement('w:instrText')
    instrText.set(qn('xml:space'), 'preserve')
    instrText.text = f' {fmt} '
    fldChar2 = OxmlElement('w:fldChar')
    fldChar2.set(qn('w:fldCharType'), 'end')
    run._r.append(fldChar)
    run._r.append(instrText)
    run._r.append(fldChar2)


def _set_page_num_format(section, fmt='lowerRoman', start=1):
    """
    Đặt định dạng số trang cho 1 section.
    fmt: 'lowerRoman' → i,ii,iii | 'decimal' → 1,2,3
    start: số trang bắt đầu
    """
    sectPr = section._sectPr
    pgNumType = OxmlElement('w:pgNumType')
    pgNumType.set(qn('w:fmt'), fmt)
    pgNumType.set(qn('w:start'), str(start))
    # Xóa pgNumType cũ nếu có
    for old in sectPr.findall(qn('w:pgNumType')):
        sectPr.remove(old)
    sectPr.append(pgNumType)


def setup_header_footer(section, doc_type, ten_de_tai):
    """
    Cài Header + Footer chuẩn TDTU MauDATN_2021 — TỪ CHƯƠNG 1 TRỞ ĐI:

    HEADER (1 dòng, có gạch dưới):
        ĐỒ ÁN TỐT NGHIỆP                              Trang X
        ─────────────────────────────────────────────────────
        [Trái: tên loại ĐA]              [Phải: số trang]

    FOOTER (1 dòng, có gạch trên):
        ─────────────────────────────────────────────────────
                         TÊN ĐỀ TÀI

    NOTE: Trước Chương 1 — chỉ có số La Mã ở footer, dùng _setup_roman_footer()
    """
    from docx.shared import Cm as _Cm
    from docx.oxml import OxmlElement as _elem

    # ── HEADER: 1 dòng, Left tab = tên ĐA, Right tab = "Trang X" ──
    header = section.header
    header.is_linked_to_previous = False
    for p in header.paragraphs:
        p.clear()

    p_hdr = header.paragraphs[0]
    # TabStop: right-align ở cuối dòng text (page width − lề = ~15.5 cm)
    # Dùng w:tab + w:tabStop để có Left text và Right text trên 1 dòng
    pPr = p_hdr._p.get_or_add_pPr()

    # Đặt tab stop phải tại ~15.5 cm (A4 21cm − 3.5 lề trái − 2.0 lề phải = 15.5cm)
    tabs = OxmlElement('w:tabs')
    ts = OxmlElement('w:tab')
    ts.set(qn('w:val'), 'right')
    ts.set(qn('w:pos'), str(int(8750)))  # 8750 twips ≈ 15.5 cm
    tabs.append(ts)
    pPr.append(tabs)

    # Gạch dưới header
    pBdr = OxmlElement('w:pBdr')
    bot = OxmlElement('w:bottom')
    bot.set(qn('w:val'), 'single'); bot.set(qn('w:sz'), '6')
    bot.set(qn('w:space'), '1');    bot.set(qn('w:color'), '000000')
    pBdr.append(bot); pPr.append(pBdr)

    def _hdr_run(text, bold=False):
        r = OxmlElement('w:r')
        rPr = OxmlElement('w:rPr')
        rFonts = OxmlElement('w:rFonts')
        rFonts.set(qn('w:ascii'), 'Times New Roman')
        rFonts.set(qn('w:hAnsi'), 'Times New Roman')
        sz = OxmlElement('w:sz'); sz.set(qn('w:val'), '22')  # 11pt
        b  = OxmlElement('w:b')
        rPr.append(rFonts); rPr.append(sz)
        if bold: rPr.append(b)
        r.append(rPr)
        t = OxmlElement('w:t')
        t.set(qn('xml:space'), 'preserve')
        t.text = text
        r.append(t)
        return r

    def _tab_char():
        r = OxmlElement('w:r')
        t = OxmlElement('w:tab')
        r.append(t)
        return r

    def _page_field():
        """Field PAGE tự động."""
        r = OxmlElement('w:r')
        rPr = OxmlElement('w:rPr')
        rFonts = OxmlElement('w:rFonts')
        rFonts.set(qn('w:ascii'), 'Times New Roman')
        rFonts.set(qn('w:hAnsi'), 'Times New Roman')
        sz = OxmlElement('w:sz'); sz.set(qn('w:val'), '22')
        rPr.append(rFonts); rPr.append(sz)
        r.append(rPr)
        fc1 = OxmlElement('w:fldChar'); fc1.set(qn('w:fldCharType'), 'begin')
        it  = OxmlElement('w:instrText')
        it.set(qn('xml:space'), 'preserve'); it.text = ' PAGE '
        fc2 = OxmlElement('w:fldChar'); fc2.set(qn('w:fldCharType'), 'end')
        r.append(fc1); r.append(it); r.append(fc2)
        return r

    # Trái: tên loại ĐA | Tab | Phải: "Trang " + số trang
    p_hdr._p.append(_hdr_run(doc_type.upper(), bold=True))
    p_hdr._p.append(_tab_char())
    p_hdr._p.append(_hdr_run('Trang '))
    p_hdr._p.append(_page_field())

    # ── FOOTER: tên đề tài căn giữa, gạch trên ──
    footer = section.footer
    footer.is_linked_to_previous = False
    for p in footer.paragraphs:
        p.clear()

    p_ftr = footer.paragraphs[0]
    p_ftr.alignment = WD_ALIGN_PARAGRAPH.CENTER

    # Gạch trên footer
    pPr_f = p_ftr._p.get_or_add_pPr()
    pBdr_f = OxmlElement('w:pBdr')
    top = OxmlElement('w:top')
    top.set(qn('w:val'), 'single'); top.set(qn('w:sz'), '6')
    top.set(qn('w:space'), '1');   top.set(qn('w:color'), '000000')
    pBdr_f.append(top); pPr_f.append(pBdr_f)

    run_title = p_ftr.add_run(ten_de_tai.upper())
    run_title.font.name = 'Times New Roman'
    run_title.font.size = Pt(11)
    run_title.font.bold = True


def add_section_break_before_chapter1(doc, doc_type, ten_de_tai):
    """
    Chèn Section Break (Next Page) trước Chương 1 để bắt đầu đánh số Ả Rập và hiện Header.
    """
    from docx.enum.section import WD_SECTION
    
    # Tạo section mới thay vì append XML thủ công
    new_section = doc.add_section(WD_SECTION.NEW_PAGE)
    
    # Cài đặt số trang Ả Rập, bắt đầu lại từ 1
    _set_page_num_format(new_section, fmt='decimal', start=1)

    # Cài lại header/footer cho section mới (Chương 1 trở đi)
    new_section.top_margin    = Cm(3.5)
    new_section.bottom_margin = Cm(3.0)
    new_section.left_margin   = Cm(3.5)
    new_section.right_margin  = Cm(2.0)
    new_section.header_linked_to_previous = False
    new_section.footer_linked_to_previous = False
    setup_header_footer(new_section, doc_type, ten_de_tai)


def _setup_roman_footer(section):
    """Footer chỉ có số La Mã căn giữa — cho các trang phần đầu (Bìa 2 → trước Chương 1)."""
    footer = section.footer
    footer.is_linked_to_previous = False
    for p in footer.paragraphs:
        p.clear()
    p_num = footer.paragraphs[0]
    p_num.alignment = WD_ALIGN_PARAGRAPH.CENTER
    # Chỉ có field số trang (La Mã) — không có gạch, không có tiêu đề
    r_field = OxmlElement('w:r')
    rPr = OxmlElement('w:rPr')
    rFonts = OxmlElement('w:rFonts')
    rFonts.set(qn('w:ascii'), 'Times New Roman')
    rFonts.set(qn('w:hAnsi'), 'Times New Roman')
    sz = OxmlElement('w:sz'); sz.set(qn('w:val'), '26')
    rPr.append(rFonts); rPr.append(sz)
    r_field.append(rPr)
    fc1 = OxmlElement('w:fldChar'); fc1.set(qn('w:fldCharType'), 'begin')
    it  = OxmlElement('w:instrText')
    it.set(qn('xml:space'), 'preserve')
    it.text = ' PAGE \\* lowerRoman '   # hiển thị i ii iii iv...
    fc2 = OxmlElement('w:fldChar'); fc2.set(qn('w:fldCharType'), 'end')
    r_field.append(fc1); r_field.append(it); r_field.append(fc2)
    p_num._p.append(r_field)


# ──────────────────────────────────────────────────────────────────
# EQUATION ENGINE — Word OMML (Office Math Markup Language)
# Render công thức toán học đẹp, đều cỡ, ký tự đặc biệt thật sự
# ──────────────────────────────────────────────────────────────────

# Namespace OMML
OMML_NS = 'http://schemas.openxmlformats.org/officeDocument/2006/math'
W_NS    = 'http://schemas.openxmlformats.org/wordprocessingml/2006/main'

def _m(tag: str):
    """Tạo element trong namespace OMML (m:)."""
    return OxmlElement(f'm:{tag}')

def _omml_run(text: str, italic=True, size_pt=13) -> 'Element':
    """Tạo 1 m:r (run toán học) chứa ký tự."""
    r   = _m('r')
    rpr = _m('rPr')
    # Font chữ math
    rFonts = OxmlElement('w:rFonts')
    rFonts.set(qn('w:ascii'), 'Cambria Math')
    rFonts.set(qn('w:hAnsi'), 'Cambria Math')
    sz = OxmlElement('w:sz');  sz.set(qn('w:val'), str(size_pt * 2))
    i_el = _m('sty'); i_el.set(qn('m:val'), 'i' if italic else 'p')  # italic / plain
    rpr.append(rFonts); rpr.append(sz); rpr.append(i_el)
    r.append(rpr)
    t = _m('t'); t.text = text
    r.append(t)
    return r

def _omml_frac(num_els, den_els) -> 'Element':
    """Tạo phân số m:f với tử num_els và mẫu den_els."""
    f    = _m('f')
    fPr  = _m('fPr'); ftype = _m('type'); ftype.set(qn('m:val'), 'bar'); fPr.append(ftype)
    num  = _m('num')
    den  = _m('den')
    for el in num_els: num.append(el)
    for el in den_els: den.append(el)
    f.append(fPr); f.append(num); f.append(den)
    return f

def _omml_sub(base_els, sub_els) -> 'Element':
    """Tạo chỉ số dưới: base_{sub}."""
    sScript = _m('sSub')
    sPr     = _m('sSubPr'); ctrl = _m('ctrlPr'); sPr.append(ctrl)
    e  = _m('e'); [e.append(b) for b in base_els]
    sub= _m('sub'); [sub.append(s) for s in sub_els]
    sScript.append(sPr); sScript.append(e); sScript.append(sub)
    return sScript

def _omml_sup(base_els, sup_els) -> 'Element':
    """Tạo chỉ số trên: base^{sup}."""
    sScript = _m('sSup')
    sPr     = _m('sSupPr'); ctrl = _m('ctrlPr'); sPr.append(ctrl)
    e  = _m('e'); [e.append(b) for b in base_els]
    sup= _m('sup'); [sup.append(s) for s in sup_els]
    sScript.append(sPr); sScript.append(e); sScript.append(sup)
    return sScript

def _omml_subsup(base_els, sub_els, sup_els) -> 'Element':
    """Tạo cả sub và sup cùng lúc: base_{sub}^{sup}."""
    sScript = _m('sSubSup')
    sPr     = _m('sSubSupPr'); ctrl = _m('ctrlPr'); sPr.append(ctrl)
    e   = _m('e');   [e.append(b) for b in base_els]
    sub = _m('sub'); [sub.append(s) for s in sub_els]
    sup = _m('sup'); [sup.append(s) for s in sup_els]
    sScript.append(sPr); sScript.append(e); sScript.append(sub); sScript.append(sup)
    return sScript

def _omml_sqrt(inner_els) -> 'Element':
    """Căn bậc 2."""
    rad = _m('rad')
    radPr = _m('radPr'); deg = _m('deg'); radPr.append(deg)  # no degree = sqrt
    e = _m('e'); [e.append(el) for el in inner_els]
    rad.append(radPr); rad.append(e)
    return rad

# Bảng ký tự đặc biệt LaTeX → Unicode (dùng trong _omml_run)
GREEK = {
    'omega': 'ω', 'Omega': 'Ω', 'theta': 'θ', 'Theta': 'Θ',
    'alpha': 'α', 'beta': 'β', 'gamma': 'γ', 'Gamma': 'Γ',
    'delta': 'δ', 'Delta': 'Δ', 'epsilon': 'ε', 'zeta': 'ζ',
    'eta': 'η', 'pi': 'π', 'Pi': 'Π', 'rho': 'ρ', 'sigma': 'σ',
    'Sigma': 'Σ', 'tau': 'τ', 'phi': 'φ', 'Phi': 'Φ', 'chi': 'χ',
    'psi': 'ψ', 'Psi': 'Ψ', 'mu': 'μ', 'nu': 'ν', 'xi': 'ξ',
    'lambda': 'λ', 'Lambda': 'Λ', 'kappa': 'κ', 'iota': 'ι',
}
OPERATORS = {
    'times': '×', 'div': '÷', 'pm': '±', 'mp': '∓',
    'approx': '≈', 'neq': '≠', 'leq': '≤', 'geq': '≥',
    'cdot': '·', 'dot': '·', 'infty': '∞', 'sum': 'Σ',
    'prod': 'Π', 'int': '∫', 'partial': '∂', 'nabla': '∇',
    'in': '∈', 'notin': '∉', 'forall': '∀', 'exists': '∃',
    'rightarrow': '→', 'leftarrow': '←', 'Rightarrow': '⇒',
    'cos': 'cos', 'sin': 'sin', 'tan': 'tan',
}

def _tex_sym(sym: str) -> str:
    """Chuyển tên ký tự LaTeX → Unicode. VD: 'omega' → 'ω'."""
    return GREEK.get(sym) or OPERATORS.get(sym) or sym


def add_equation(doc, latex_like: str, caption: str = '', label: str = '', center=True):
    """
    Chèn công thức toán học vào Word dùng OMML (Cambria Math, đúng cỡ, đều nhau).

    Cú pháp `latex_like` đơn giản (không cần gói LaTeX):
      - Ký tự Greek: \\omega \\theta \\Delta  → ω θ Δ
      - Phân số:     FRAC(a+b)(c)
      - Chỉ số dưới: x_{k+1}   SUB(x)(k+1)
      - Chỉ số trên: x^{2}     SUP(x)(2)
      - Căn:         SQRT(expr)
      - Ký tự bình thường viết thẳng

    Ví dụ:
      add_equation(doc, "v = FRAC(\\omega_R + \\omega_L)(2) × r")
      add_equation(doc, "SUB(x)(k+1) = SUB(x)(k) + v·cos(θ)·Δt")

    Nếu có `caption`, chèn thêm dòng "Phương trình X.Y: ..." bên dưới.
    """
    # ── Xây dựng cây OMML từ latex_like ──
    # Vì parser đầy đủ rất phức tạp, ta dùng phương pháp thực dụng:
    # Chuyển tất cả ký tự đặc biệt → Unicode, rồi nhúng vào m:oMath
    import re

    # Bước 1: thay thế ký tự đặc biệt
    text = latex_like
    for name, sym in {**GREEK, **OPERATORS}.items():
        text = text.replace(f'\\{name}', sym)

    # Bước 2: tạo oMath element đơn giản (plain math với Unicode chars)
    p = doc.add_paragraph()
    if center:
        p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    else:
        p.alignment = WD_ALIGN_PARAGRAPH.LEFT

    # Thêm oMath với Cambria Math
    oMath = OxmlElement('m:oMath')
    oMath.set('xmlns:m', OMML_NS)

    # Parse FRAC(...)(...)  SUB(...)(...)  SUP(...)(...)  SQRT(...)
    def parse_and_build(expr: str) -> list:
        """Trả về list of OMML elements từ chuỗi expr."""
        parts = []
        i = 0
        tok_re = re.compile(
            r'FRAC\(([^)]*)\)\(([^)]*)\)'
            r'|SUB\(([^)]*)\)\(([^)]*)\)'
            r'|SUP\(([^)]*)\)\(([^)]*)\)'
            r'|SQRT\(([^)]*)\)'
            r'|([^FSf]+)'
        )
        for m in tok_re.finditer(expr):
            if m.group(1) is not None:           # FRAC
                num = [_omml_run(m.group(1))]
                den = [_omml_run(m.group(2))]
                parts.append(_omml_frac(num, den))
            elif m.group(3) is not None:          # SUB
                base = [_omml_run(m.group(3))]
                sub  = [_omml_run(m.group(4), italic=False)]
                parts.append(_omml_sub(base, sub))
            elif m.group(5) is not None:          # SUP
                base = [_omml_run(m.group(5))]
                sup  = [_omml_run(m.group(6), italic=False)]
                parts.append(_omml_sup(base, sup))
            elif m.group(7) is not None:          # SQRT
                inner= [_omml_run(m.group(7))]
                parts.append(_omml_sqrt(inner))
            elif m.group(8) is not None:          # plain text
                if m.group(8).strip():
                    parts.append(_omml_run(m.group(8)))
        return parts

    for el in parse_and_build(text):
        oMath.append(el)

    p._p.append(oMath)

    # Thêm dòng caption (số phương trình)
    if caption:
        pc = doc.add_paragraph(caption)
        pc.alignment = WD_ALIGN_PARAGRAPH.CENTER
        run = pc.runs[0]
        run.font.name = 'Times New Roman'
        run.font.size = Pt(12)
        run.font.italic = True

    return p


def insert_kinematic_equations(doc):
    """
    Chèn đúng các phương trình động học robot 2 bánh — chuẩn TDTU.
    Đây là ví dụ mẫu cho Chương 3/4.

    Kết quả render:
        v  = (ωR + ωL) / 2 × r
        w  = (ωR − ωL) × r / L

    Odometry:
        x[k+1] = x[k] + v·cos(θ[k])·Δt
        y[k+1] = y[k] + v·sin(θ[k])·Δt
        θ[k+1] = θ[k] + w[k]·Δt
    """
    intro = doc.add_paragraph(
        '    Từ vận tốc góc hai bánh (ωL, ωR), robot tính vận tốc tuyến tính v '
        'và vận tốc góc w theo công thức kinematics vi sai:'
    )
    intro.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
    for r in intro.runs:
        r.font.name = 'Times New Roman'; r.font.size = Pt(13)

    # v = (ωR + ωL) / 2 × r
    add_equation(doc, 'v = FRAC(ωR + ωL)(2) × r',
                 caption='Phương trình 3.1: Vận tốc tuyến tính robot')
    # w = (ωR − ωL) × r / L
    add_equation(doc, 'w = FRAC((ωR − ωL) × r)(L)',
                 caption='Phương trình 3.2: Vận tốc góc robot')

    doc.add_paragraph('    Cập nhật odometry (x, y, θ) theo phương trình tích phân rời rạc với Δt = 20ms:')

    # x[k+1] = x[k] + v·cos(θ[k])·Δt
    add_equation(doc, 'SUB(x)(k+1) = SUB(x)(k) + v · cos(SUB(θ)(k)) · Δt',
                 caption='Phương trình 3.3: Cập nhật tọa độ x')
    add_equation(doc, 'SUB(y)(k+1) = SUB(y)(k) + v · sin(SUB(θ)(k)) · Δt',
                 caption='Phương trình 3.4: Cập nhật tọa độ y')
    add_equation(doc, 'SUB(θ)(k+1) = SUB(θ)(k) + SUB(w)(k) · Δt',
                 caption='Phương trình 3.5: Cập nhật góc hướng')


def download_tdtu_logo():
    """Tải logo TDTU từ Wikipedia về temp folder nếu chưa có."""
    logo_path = os.path.join(tempfile.gettempdir(), 'tdtu_logo.png')
    if os.path.exists(logo_path):
        return logo_path
    try:
        import requests
        url = "https://upload.wikimedia.org/wikipedia/vi/1/1b/TDTU_logo.png"
        resp = requests.get(url, timeout=10)
        if resp.status_code == 200:
            with open(logo_path, 'wb') as f:
                f.write(resp.content)
            return logo_path
    except:
        pass
    return None


def create_cover_page(doc, ten_de_tai, sinh_vien, mssv, gvhd, chuyen_nganh, nam, logo_path=None):
    """Tạo 1 trang bìa chuẩn TDTU."""
    # Header trường
    p = doc.add_paragraph('TỔNG LIÊN ĐOÀN LAO ĐỘNG VIỆT NAM')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13)
    
    p = doc.add_paragraph('TRƯỜNG ĐẠI HỌC TÔN ĐỨC THẮNG')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13); run.font.bold = True
    
    p = doc.add_paragraph(f'KHOA {chuyen_nganh.upper()}')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13); run.font.bold = True
    
    # Logo TDTU
    if logo_path:
        p = doc.add_paragraph()
`
