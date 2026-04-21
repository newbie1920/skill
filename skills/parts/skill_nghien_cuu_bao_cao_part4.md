# Phần 4/4: Generator Script - Assembling Logic & Adaptive Behavior
> 💡 **Chú ý cho AI:** Đây là phần 4 của Skill Báo Cáo. Bạn cần đọc 4 phần để hoạt động chính xác.
`python

        p.alignment = WD_ALIGN_PARAGRAPH.CENTER
        run = p.add_run()
        run.add_picture(logo_path, width=Cm(4.5))  # Logo kích thước mỏng ở giữa
        doc.add_paragraph()
    else:
        doc.add_paragraph()
        doc.add_paragraph()
    
    # Tên sinh viên
    p = doc.add_paragraph(f"{sinh_vien.upper()} ({mssv})")
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(14); run.font.bold = True
    
    doc.add_paragraph()
    doc.add_paragraph()
    
    # Tên đề tài
    p = doc.add_paragraph(ten_de_tai.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(22); run.font.bold = True
    
    doc.add_paragraph()
    doc.add_paragraph()
    
    p = doc.add_paragraph('ĐỒ ÁN TỐT NGHIỆP / CHUYÊN NGÀNH NÂNG CAO')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(14); run.font.bold = True
    
    p = doc.add_paragraph(chuyen_nganh.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(14); run.font.bold = True
    
    doc.add_paragraph()
    doc.add_paragraph()
    doc.add_paragraph()
    
    p = doc.add_paragraph(f'Người hướng dẫn: {gvhd}')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(14)
    
    doc.add_paragraph()
    doc.add_paragraph()
    
    p = doc.add_paragraph(f'TP. HỒ CHÍ MINH, NĂM {nam}')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13); run.font.bold = True
    

def _set_page_num_suppress(section):
    """Tắt số trang cho 1 section (dùng cho 2 trang bìa ngoài)."""
    sectPr = section._sectPr
    pgNumType = sectPr.find(qn('w:pgNumType'))
    if pgNumType is None:
        pgNumType = OxmlElement('w:pgNumType')
        sectPr.append(pgNumType)
    # Word không có "suppress" trực tiếp — ẩn header/footer là đủ
    # Thay vào đó: không đánh số bằng cách set titlePg
    titlePg = OxmlElement('w:titlePg')
    sectPr.append(titlePg)


def create_bia_ngoai(doc, ten_de_tai, sinh_vien, mssv, gvhd, chuyen_nganh,
                    loai_do_an, nam, logo_path=None):
    """Tạo Bìa 1 (Bìa ngoài) — KHÔNG có số trang — chuẩn MauDATN_2021."""
    # ── Dòng trường ──
    for text, bold, size in [
        ('TỔNG LIÊN ĐOÀN LAO ĐỘNG VIỆT NAM', False, 14),
        ('TRƯỜNG ĐẠI HỌC TÔN ĐỨC THẮNG',    True,  14),
        (f'KHOA {chuyen_nganh.upper()}',       True,  14),
    ]:
        p = doc.add_paragraph(text)
        p.alignment = WD_ALIGN_PARAGRAPH.CENTER
        run = p.runs[0]
        run.font.name = 'Times New Roman'
        run.font.size = Pt(size)
        run.font.bold = bold

    # ── Logo TDTU ──
    if logo_path and os.path.exists(logo_path):
        p_logo = doc.add_paragraph()
        p_logo.alignment = WD_ALIGN_PARAGRAPH.CENTER
        p_logo.paragraph_format.space_before = Pt(18)
        p_logo.paragraph_format.space_after  = Pt(18)
        p_logo.add_run().add_picture(logo_path, width=Cm(4.0))
    else:
        # Placeholder text nếu không tải được logo
        p = doc.add_paragraph('[ LOGO TDTU ]')
        p.alignment = WD_ALIGN_PARAGRAPH.CENTER
        p.paragraph_format.space_before = Pt(20)
        p.paragraph_format.space_after  = Pt(20)

    # ── Tên sinh viên ──
    doc.add_paragraph()
    p = doc.add_paragraph(sinh_vien.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(14); run.font.bold = True

    doc.add_paragraph()
    doc.add_paragraph()

    # ── Tên đề tài (size 22) ──
    p = doc.add_paragraph(ten_de_tai.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(22); run.font.bold = True

    doc.add_paragraph()
    doc.add_paragraph()

    # ── Loại đồ án + Chuyên ngành (size 20) ──
    p = doc.add_paragraph(loai_do_an.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(20); run.font.bold = True

    p = doc.add_paragraph(chuyen_nganh.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(20); run.font.bold = True

    doc.add_paragraph()
    doc.add_paragraph()

    # ── GVHD ──
    p = doc.add_paragraph('Người hướng dẫn:')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    p.runs[0].font.name = 'Times New Roman'; p.runs[0].font.size = Pt(14)

    p = doc.add_paragraph(gvhd)
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(14); run.font.bold = True

    doc.add_paragraph()
    doc.add_paragraph()

    # ── Năm ──
    p = doc.add_paragraph(f'THÀNH PHỐ HỒ CHÍ MINH, NĂM {nam}')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(14); run.font.bold = True


def create_bia_lot(doc, ten_de_tai, gvhd):
    """
    Tạo Bìa 2 (Bìa lót / Certification Page) — trang ii.
    Đây là trang XÁC NHẬN HỘI ĐỒNG, KHÔNG phải copy bìa ngoài.
    Chuẩn MauDATN_2021 TDTU.
    """
    doc.add_paragraph()

    p = doc.add_paragraph('Công trình được hoàn thành tại Trường Đại học Tôn Đức Thắng')
    p.paragraph_format.space_after = Pt(12)
    _fmt_run(p.runs[0], 13)

    p = doc.add_paragraph('Cán bộ hướng dẫn khoa học:  .......................................................................')
    _fmt_run(p.runs[0], 13)

    # Dòng chữ nghiêng ghi chú
    p2 = doc.add_paragraph()
    p2.alignment = WD_ALIGN_PARAGRAPH.RIGHT
    run = p2.add_run('(Ghi rõ học hàm, học vị, họ tên và chữ ký)')
    run.font.name = 'Times New Roman'; run.font.size = Pt(13); run.font.italic = True

    doc.add_paragraph()

    p = doc.add_paragraph()
    run1 = p.add_run('Đồ án tốt nghiệp/tổng hợp được bảo vệ tại ')
    _fmt_run_inline(run1, 13, bold=False)
    run2 = p.add_run('Hội đồng đánh giá Đồ án tốt nghiệp/tổng hợp '
                     'của Trường Đại học Tôn Đức Thắng')
    _fmt_run_inline(run2, 13, bold=True)
    run3 = p.add_run(' vào ngày… /…/……')
    _fmt_run_inline(run3, 13, bold=False)

    doc.add_paragraph()

    p = doc.add_paragraph()
    run_xn = p.add_run('Xác nhận của Chủ tịch Hội đồng đánh giá ')
    _fmt_run_inline(run_xn, 13, bold=False)
    run_red = p.add_run('Đồ án tốt nghiệp/tổng hợp và Trưởng khoa '
                        'quản lý chuyên ngành sau khi Đồ án tốt nghiệp/tổng hợp '
                        'đã được sửa chữa (nếu có).')
    run_red.font.name  = 'Times New Roman'
    run_red.font.size  = Pt(13)
    run_red.font.color.rgb = RGBColor(0xFF, 0x00, 0x00)  # Chữ đỏ như mẫu

    doc.add_paragraph()

    # ── Hàng chữ ký (2 cột: Chủ tịch HĐ | Trưởng Khoa) ──
    tbl = doc.add_table(rows=3, cols=2)
    tbl.style = 'Table Grid'
    for c in tbl.columns:
        for cell in c.cells:
            for border_name in ['top', 'left', 'bottom', 'right']:
                tc = cell._tc
                tcPr = tc.get_or_add_tcPr()
                tcBorders = OxmlElement('w:tcBorders')
                b = OxmlElement(f'w:{border_name}')
                b.set(qn('w:val'), 'none')
                tcBorders.append(b)
                tcPr.append(tcBorders)

    def _cell_bold_center(cell, text, bold=True):
        p = cell.paragraphs[0]
        p.alignment = WD_ALIGN_PARAGRAPH.CENTER
        run = p.add_run(text)
        run.font.name = 'Times New Roman'; run.font.size = Pt(13); run.font.bold = bold

    _cell_bold_center(tbl.rows[0].cells[0], 'CHỦ TỊCH HỘI ĐỒNG')
    _cell_bold_center(tbl.rows[0].cells[1], 'TRƯỞNG KHOA')
    _cell_bold_center(tbl.rows[1].cells[0], '')
    _cell_bold_center(tbl.rows[1].cells[1], '')
    _cell_bold_center(tbl.rows[2].cells[0], '................................', bold=False)
    _cell_bold_center(tbl.rows[2].cells[1], '..................................', bold=False)


def _fmt_run(run, size, bold=False, italic=False):
    """Helper nhanh cho run trong paragraph mới."""
    run.font.name  = 'Times New Roman'
    run.font.size  = Pt(size)
    run.font.bold  = bold
    run.font.italic = italic

def _fmt_run_inline(run, size, bold=False):
    run.font.name = 'Times New Roman'
    run.font.size = Pt(size)
    run.font.bold = bold


def create_cam_doan(doc, sinh_vien):
    """
    Tạo trang CAM ĐOAN — chuẩn MauDATN_2021.
    Tiêu đề ở giữa, nội dung justified, chữ ký bên phải.
    """
    p = doc.add_paragraph('CÔNG TRÌNH ĐƯỢC HOÀN THÀNH')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True

    p = doc.add_paragraph('TẠI TRƯỜNG ĐẠI HỌC TÔN ĐỨC THẮNG')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True

    doc.add_paragraph()

    body = (
        f'    Tôi xin cam đoan đây là công trình nghiên cứu của riêng tôi và được sự hướng '
        f'dẫn khoa học của ………………………………… Các nội dung nghiên cứu, kết quả trong đề tài này '
        f'là trung thực và chưa công bố dưới bất kỳ hình thức nào trước đây. Những số liệu '
        f'trong các bảng biểu phục vụ cho việc phân tích, nhận xét, đánh giá được chính tác '
        f'giả thu thập từ các nguồn khác nhau có ghi rõ trong phần tài liệu tham khảo.'
    )
    p = doc.add_paragraph(body)
    p.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13)

    doc.add_paragraph()

    body2 = (
        '    Ngoài ra, trong Đồ án tốt nghiệp/ tổng hợp còn sử dụng một số nhận xét, đánh giá '
        'cũng như số liệu của các tác giả khác, cơ quan tổ chức khác đều có trích dẫn và '
        'chú thích nguồn gốc.'
    )
    p = doc.add_paragraph(body2)
    p.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13)

    doc.add_paragraph()

    p = doc.add_paragraph()
    run1 = p.add_run('    Nếu phát hiện có bất kỳ sự gian lận nào tôi xin hoàn toàn chịu '
                     'trách nhiệm về nội dung Đồ án tốt nghiệp/ tổng hợp của mình. ')
    run1.font.name = 'Times New Roman'; run1.font.size = Pt(13); run1.font.bold = True
    run2 = p.add_run('Trường Đại học Tôn Đức Thắng không liên quan đến những vi phạm '
                     'tác quyền, bản quyền do tôi gây ra trong quá trình thực hiện (nếu có).')
    run2.font.name = 'Times New Roman'; run2.font.size = Pt(13)
    p.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY

    doc.add_paragraph()

    for sig_line in ['TP. Hồ Chí Minh, ngày    tháng    năm', 'Tác giả', f'(ký tên và ghi rõ họ tên)']:
        p = doc.add_paragraph(sig_line)
        p.alignment = WD_ALIGN_PARAGRAPH.RIGHT
        run = p.runs[0]; run.font.name = 'Times New Roman'
        run.font.size = Pt(13); run.font.italic = True


def create_nhiem_vu_da(doc):
    """Trang đính kèm Nhiệm vụ Đồ án — placeholder."""
    doc.add_paragraph()
    p = doc.add_paragraph(
        '(Trang này dùng để đính kèm Nhiệm vụ Đồ án tốt nghiệp có chữ ký '
        'của Giảng viên hướng dẫn)'
    )
    p.alignment = WD_ALIGN_PARAGRAPH.LEFT
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13)



def _add_tof_field(doc, heading_text, field_instruction):
    """Chèn Word TOF/TOC field tự động (update khi F9 trong Word)."""
    # Tiêu đề
    p_head = doc.add_paragraph(heading_text)
    p_head.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p_head.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(14); run.font.bold = True
    doc.add_paragraph()
    # TOF field
    p = doc.add_paragraph()
    fldChar_begin = OxmlElement('w:fldChar'); fldChar_begin.set(qn('w:fldCharType'), 'begin')
    instrText    = OxmlElement('w:instrText')
    instrText.set(qn('xml:space'), 'preserve')
    instrText.text = field_instruction
    fldChar_end  = OxmlElement('w:fldChar'); fldChar_end.set(qn('w:fldCharType'), 'end')
    r = OxmlElement('w:r')
    r.append(fldChar_begin); r.append(instrText); r.append(fldChar_end)
    p._p.append(r)
    doc.add_paragraph('[Nhấn Ctrl+A → F9 để Word tự điền danh mục này]')


def _add_list_of_figures(doc):
    """Chèn trang DANH MỤC HÌNH VẼ dùng Word TOF field (Figure captions)."""
    _add_tof_field(doc, 'DANH MỤC HÌNH VẼ',
                   ' TOC \\h \\z \\t "Caption" ')


def _add_list_of_tables(doc):
    """Chèn trang DANH MỤC BẢNG BIỂU dùng Word TOF field (Table captions)."""
    _add_tof_field(doc, 'DANH MỤC BẢNG BIỂU',
                   ' TOC \\h \\z \\t "Caption" ')


def create_tom_tat(doc, ten_de_tai):
    """
    Tạo trang TÓM TẮT — chuẩn MauDATN_2021.
    Tiêu đề đề tài + TÓM TẮT (Bold, 16pt) căn giữa, rồi dấu chấm chờ.
    """
    doc.add_paragraph()
    doc.add_paragraph()
    doc.add_paragraph()

    p = doc.add_paragraph(ten_de_tai.upper())
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True

    p = doc.add_paragraph('TÓM TẮT')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True

    p = doc.add_paragraph('(Bold, Size 16)')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True

    doc.add_paragraph()

    # Dấu chấm chờ — 5 dòng
    dot_line = '(Times New Roman – 13) ' + '…' * 55
    for i, line in enumerate([dot_line] + ['…' * 63] * 4):
        p = doc.add_paragraph(line)
        p.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
        run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13)


def create_lich_trinh_da(doc, ten_de_tai, sinh_vien, mssv, chuyen_nganh):
    """
    Tạo trang LỊCH TRÌNH LÀM ĐỒ ÁN TỐT NGHIỆP — chuẩn MauDATN_2021.
    Gồm: header 2 cột, tiêu đề, thông tin SV, bảng 4 cột lớn.
    """
    from docx.oxml import OxmlElement
    from docx.oxml.ns import qn

    def _set_cell_borders(cell, **kwargs):
        tc = cell._tc
        tcPr = tc.get_or_add_tcPr()
        tcBorders = OxmlElement('w:tcBorders')
        for edge in ('top', 'left', 'bottom', 'right', 'insideH', 'insideV'):
            tag = OxmlElement(f'w:{edge}')
            tag.set(qn('w:val'), kwargs.get(edge, 'single'))
            tag.set(qn('w:sz'),  kwargs.get('sz', '6'))
            tag.set(qn('w:color'), '000000')
            tcBorders.append(tag)
        tcPr.append(tcBorders)

    def _cell_text(cell, text, bold=False, center=False, size=13):
        p = cell.paragraphs[0] if cell.paragraphs else cell.add_paragraph()
        p.alignment = WD_ALIGN_PARAGRAPH.CENTER if center else WD_ALIGN_PARAGRAPH.LEFT
        run = p.add_run(text)
        run.font.name = 'Times New Roman'; run.font.size = Pt(size); run.font.bold = bold

    def _merge_and_write(tbl, row_idx, col_start, col_end, text, bold=False, center=True):
        row = tbl.rows[row_idx]
        cell = row.cells[col_start]
        if col_start != col_end:
            cell = cell.merge(row.cells[col_end])
        _cell_text(cell, text, bold=bold, center=center)
        return cell

    # ── Header trường (2 cột) bằng bảng 1 hàng ──
    tbl_hdr = doc.add_table(rows=1, cols=2)
    tbl_hdr.style = 'Table Grid'
    left_cell  = tbl_hdr.rows[0].cells[0]
    right_cell = tbl_hdr.rows[0].cells[1]
    for cell in [left_cell, right_cell]:
        for border in ['top','left','bottom','right']:
            tc = cell._tc; tcPr = tc.get_or_add_tcPr()
            tcBorders = OxmlElement('w:tcBorders')
            b = OxmlElement(f'w:{border}'); b.set(qn('w:val'), 'none')
            tcBorders.append(b); tcPr.append(tcBorders)

    def _two_line_cell(cell, line1, line2='', bold1=False, bold2=False):
        p1 = cell.paragraphs[0]; p1.alignment = WD_ALIGN_PARAGRAPH.CENTER
        r1 = p1.add_run(line1); r1.font.name='Times New Roman'; r1.font.size=Pt(13); r1.font.bold=bold1
        if line2:
            p2 = cell.add_paragraph(); p2.alignment = WD_ALIGN_PARAGRAPH.CENTER
            r2 = p2.add_run(line2); r2.font.name='Times New Roman'; r2.font.size=Pt(13); r2.font.bold=bold2

    _two_line_cell(left_cell,  'TRƯỜNG ĐẠI HỌC TÔN ĐỨC THẮNG',
                               f'KHOA {chuyen_nganh.upper()}', bold1=True, bold2=True)
    _two_line_cell(right_cell, 'CỘNG HÒA XÃ HỘI CHỦ NGHĨA VIỆT NAM',
                               'Độc lập – Tự do – Hạnh phúc')

    # Gạch dưới tên Khoa và Độc lập...
    for cell in [left_cell, right_cell]:
        for p in cell.paragraphs:
            if p.text:
                pBdr = OxmlElement('w:pBdr')
                bottom = OxmlElement('w:bottom')
                bottom.set(qn('w:val'), 'single'); bottom.set(qn('w:sz'), '4')
                bottom.set(qn('w:space'), '1'); bottom.set(qn('w:color'), '000000')
                pBdr.append(bottom)
                p._p.get_or_add_pPr().append(pBdr)
                break  # Chỉ gạch dòng thứ 2 (tên Khoa)

    doc.add_paragraph()

    # ── Tiêu đề ──
    p = doc.add_paragraph('LỊCH TRÌNH LÀM ĐỒ ÁN TỐT NGHIỆP')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name='Times New Roman'; run.font.size=Pt(14); run.font.bold=True

    doc.add_paragraph()

    # ── Thông tin sinh viên ──
    for line in [
        f'Họ tên sinh viên: {"." * 60}',
        f'Lớp: {"." * 40}  MSSV: {mssv}',
        f'Tên đề tài: {ten_de_tai}',
    ]:
        p = doc.add_paragraph(line)
        run = p.runs[0]; run.font.name='Times New Roman'; run.font.size=Pt(13)

    doc.add_paragraph()

    # ── Bảng lịch trình ──
    # Cấu trúc: 4 cột: [Tuần/Ngày | Đã thực hiện | Tiếp tục thực hiện | GVHD ký]
    # Hàng 0: header (merged Khối lượng = cột 1+2)
    NUM_WEEKS = 8   # 8 tuần bình thường
    total_rows = 1 + 1 + NUM_WEEKS + 1 + 1 + 4  # header-sub + header + weeks + kiểm tra + nộp + extra
    tbl = doc.add_table(rows=total_rows, cols=4)
    tbl.style = 'Table Grid'

    # Hàng 0: Tuần/Ngày | [Khối lượng merged] | GVHD ký
    tbl.rows[0].cells[0].merge(tbl.rows[1].cells[0])  # Tuần/Ngày span 2 rows
    tbl.rows[0].cells[3].merge(tbl.rows[1].cells[3])  # GVHD ký span 2 rows
    _cell_text(tbl.rows[0].cells[0], 'Tuần/Ngày', bold=True, center=True)
    khoi_luong_cell = tbl.rows[0].cells[1].merge(tbl.rows[0].cells[2])
    _cell_text(khoi_luong_cell, 'Khối lượng', bold=True, center=True)
    _cell_text(tbl.rows[0].cells[3], 'GVHD ký', bold=True, center=True)

    # Hàng 1: sub-header
    _cell_text(tbl.rows[1].cells[1], 'Đã thực hiện', bold=True, center=True)
    _cell_text(tbl.rows[1].cells[2], 'Tiếp tục thực hiện', bold=True, center=True)

    # Hàng 2 → 9: các tuần (để trống)
    for i in range(NUM_WEEKS):
        for j in range(4):
            _cell_text(tbl.rows[2+i].cells[j], '', center=True)

    # Hàng kiểm tra giữa kỳ (merged cột 0+1 cho ô nội dung)
    ki_row = tbl.rows[2 + NUM_WEEKS]
    ki_left = ki_row.cells[0]
    _cell_text(ki_left, 'Kiểm tra giữa kỳ', bold=False, center=False)
    ki_merged = ki_row.cells[1].merge(ki_row.cells[2])
    _cell_text(ki_merged, 'Đánh giá khối lượng hoàn thành……..%\n'
               'được tiếp tục/không tiếp tục thực hiện ĐATN', center=False)
    _cell_text(ki_row.cells[3], '', center=True)

    # Hàng nộp đồ án
    nop_row = tbl.rows[2 + NUM_WEEKS + 1]
    _cell_text(nop_row.cells[0], 'Nộp Đồ án tốt\nnghiệp', bold=False)
    nop_merged = nop_row.cells[1].merge(nop_row.cells[2])
    _cell_text(nop_merged,
               'Đã hoàn thành……..% Đồ án tốt nghiệp\n'
               'được bảo vệ/không được bảo vệ ĐATN', center=False)
    _cell_text(nop_row.cells[3], '')

    # Các hàng trống còn lại
    for i in range(4):
        for j in range(4):
            _cell_text(tbl.rows[2 + NUM_WEEKS + 2 + i].cells[j], '')


def tao_bao_cao_tdtu(ten_de_tai, sinh_vien, mssv, gvhd, chuyen_nganh,
                     loai_do_an="ĐỒ ÁN TỐT NGHIỆP", nam="2026", file_name="Bao_Cao_TDTU.docx"):
    """
    Hàm tạo báo cáo Word chuẩn MauDATN_2021 TDTU.
    """
    from docx.enum.section import WD_SECTION

    doc = Document()

    # ===== 1. LỀ TRANG =====
    for section in doc.sections:
        section.top_margin    = Cm(3.5)
        section.bottom_margin = Cm(3.0)
        section.left_margin   = Cm(3.5)
        section.right_margin  = Cm(2.0)

    # ===== 2. STYLES =====
    setup_styles(doc)

    # ===== 3. SECTION 1 — BÌA 1 & 2: Không có số trang =====
    section1 = doc.sections[0]
    section1.top_margin    = Cm(3.5)
    section1.bottom_margin = Cm(3.0)
    section1.left_margin   = Cm(3.5)
    section1.right_margin  = Cm(2.0)
    # Ẩn header/footer cho trang bìa 1
    hdr = section1.header
    hdr.is_linked_to_previous = False
    for p in hdr.paragraphs: p.clear()
    ftr = section1.footer
    ftr.is_linked_to_previous = False
    for p in ftr.paragraphs: p.clear()

    # ===== 4. BÌA 1 (Trang bìa ngoài — không đánh số) =====
    logo_path = download_tdtu_logo()
    create_bia_ngoai(doc, ten_de_tai, sinh_vien, mssv, gvhd,
                     chuyen_nganh, loai_do_an, nam, logo_path)

    # ── Section break sau Bìa 1 → Bìa 2 (số La Mã, bắt đầu từ ii) ──
    # Phải tạo MỚI section thực sự để tách Header/Footer
    sec_front = doc.add_section(WD_SECTION.NEW_PAGE)
    
    # ===== 5. BÌA 2 (Certification Page — số La Mã ii) =====
    sec_front.top_margin    = Cm(3.5)
    sec_front.bottom_margin = Cm(3.0)
    sec_front.left_margin   = Cm(3.5)
    sec_front.right_margin  = Cm(2.0)
    sec_front.header_linked_to_previous = False
    sec_front.footer_linked_to_previous = False
    
    # Header trống
    for p in sec_front.header.paragraphs: p.clear()
    
    # Footer: chỉ số La Mã căn giữa, bắt đầu từ ii
    _set_page_num_format(sec_front, fmt='lowerRoman', start=2)
    _setup_roman_footer(sec_front)

    create_bia_lot(doc, ten_de_tai, gvhd)
    doc.add_page_break()

    # ===== 6. LỜI CẢM ƠN (trang iii) =====
    p = doc.add_paragraph('LỜI CẢM ƠN')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True
    doc.add_paragraph()
    lco_body = (
        f'    Tôi xin chân thành cảm ơn Quý Thầy/Cô Trường Đại học Tôn Đức Thắng '
        f'đã truyền đạt những kiến thức nền tảng vô cùng quý báu trong suốt những năm học vừa qua.\n\n'
        f'    Đặc biệt, tôi xin gửi lời tri ân sâu sắc đến {gvhd} — người đã tận tình '
        f'hướng dẫn, định hướng và hỗ trợ tôi trong suốt quá trình thực hiện đề tài.\n\n'
        f'    Xin cảm ơn gia đình và bạn bè đã luôn động viên, tạo điều kiện để tôi hoàn thành tốt đồ án này.'
    )
    p = doc.add_paragraph(lco_body)
    p.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
    run = p.runs[0]; run.font.name = 'Times New Roman'; run.font.size = Pt(13)
    doc.add_paragraph()
    for sig in ['TP. Hồ Chí Minh, ngày    tháng    năm', 'Tác giả', '(Ký tên và ghi rõ họ tên)']:
        p = doc.add_paragraph(sig)
        p.alignment = WD_ALIGN_PARAGRAPH.RIGHT
        run = p.runs[0]; run.font.name = 'Times New Roman'
        run.font.size = Pt(13); run.font.italic = True
    doc.add_page_break()

    # ===== 7 & 8. CÔNG TRÌNH ĐƯỢC HOÀN THÀNH (2 trang: iv + v) =====
    # Trang iv: Hội đồng xác nhận (create_bia_lot style 2)
    # Trang v:  Cam đoan tác giả (create_cam_doan)
    create_cam_doan(doc, sinh_vien)
    doc.add_page_break()

    # ===== 9. TRANG ĐÍNH KÈM NHIỆM VỤ GVHD (trang vi) =====
    create_nhiem_vu_da(doc)
    doc.add_page_break()

    # ===== 10. LỊCH TRÌNH LÀM ĐỒ ÁN (trang vii - viii) =====
    create_lich_trinh_da(doc, ten_de_tai, sinh_vien, mssv, chuyen_nganh)
    doc.add_page_break()

    # ===== 11. TÊN ĐỀ TÀI & TÓM TẮT =====
    create_tom_tat(doc, ten_de_tai)
    doc.add_page_break()

    # ===== 12. MỤC LỤC =====
    add_toc(doc, title='MỤC LỤC')
    doc.add_page_break()

    # ===== 13. DANH MỤC HÌNH VẼ (Word TOF field) =====
    _add_list_of_figures(doc)
    doc.add_page_break()

    # ===== 14. DANH MỤC BẢNG BIỂU (Word TOF field) =====
    _add_list_of_tables(doc)
    doc.add_page_break()

    # ===== 15. DANH MỤC CÁC CHỮ VIẾT TẮT =====
    p = doc.add_paragraph('DANH MỤC CÁC CHỮ VIẾT TẮT')
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    run = p.runs[0]; run.font.name = 'Times New Roman'
    run.font.size = Pt(16); run.font.bold = True
    doc.add_paragraph()
    abbr_table = doc.add_table(rows=1, cols=3)
    abbr_table.style = 'Table Grid'
    hdr_cells = abbr_table.rows[0].cells
    for i, txt in enumerate(['Viết tắt', 'Tiếng Anh / Tiếng Việt đầy đủ', 'Nghĩa']):
        hdr_cells[i].text = txt
        r = hdr_cells[i].paragraphs[0].runs[0]
        r.font.bold = True; r.font.name = 'Times New Roman'; r.font.size = Pt(13)
    for abbr, full, meaning in [
        ('MCU', 'Microcontroller Unit', 'Vi điều khiển'),
        ('MQTT', 'Message Queuing Telemetry Transport', 'Giao thức truyền tin IoT nhẹ'),
        ('REST', 'Representational State Transfer', 'Kiến trúc API web'),
        ('JSON', 'JavaScript Object Notation', 'Định dạng dữ liệu'),
        ('GPIO', 'General Purpose Input/Output', 'Chân I/O đa năng'),
    ]:
        row = abbr_table.add_row().cells
        row[0].text = abbr; row[1].text = full; row[2].text = meaning
    doc.add_page_break()

    # ===== 16. NỘI DUNG — ĐỔI SECTION: SỐ TRANG Ả RẬP + HEADER + FOOTER =====
    add_section_break_before_chapter1(doc, loai_do_an, ten_de_tai)
    doc.add_heading('CHƯƠNG 1. GIỚI THIỆU ĐỀ TÀI', level=1)
    
    doc.add_heading('1.1 Giới thiệu đề tài', level=2)
    doc.add_paragraph('[Nội dung 1.1 — Bối cảnh thực tế, lý do chọn đề tài...]')
    
    doc.add_heading('1.2 Mục tiêu nghiên cứu', level=2)
    doc.add_paragraph('[Nội dung 1.2 — Các mục tiêu cụ thể, đo lường được...]')
    
    doc.add_heading('1.3 Đối tượng và phạm vi', level=2)
    doc.add_paragraph('[Nội dung 1.3 — Phần cứng, phần mềm sử dụng, giới hạn đề tài...]')
    
    doc.add_heading('1.4 Phương pháp tiếp cận', level=2)
    doc.add_paragraph('[Nội dung 1.4 — Kiến trúc 3 lớp / pipeline / phương pháp nghiên cứu...]')
    
    doc.add_page_break()
    
    # ===== 10. CHƯƠNG 2 =====
    doc.add_heading('CHƯƠNG 2. CƠ SỞ LÝ THUYẾT', level=1)
    doc.add_heading('2.1 [Nền tảng lý thuyết 1]', level=2)
    doc.add_paragraph('[Điền lý thuyết cốt lõi — VD: Kinematics, SLAM, PID, WebSockets...]')
    doc.add_heading('2.2 [Nền tảng lý thuyết 2]', level=2)
    doc.add_paragraph('[Điền lý thuyết tiếp theo...]')
    doc.add_page_break()
    
    # ===== 11. CHƯƠNG 3 =====
    doc.add_heading('CHƯƠNG 3. THIẾT KẾ PHẦN CỨNG', level=1)
    doc.add_heading('3.1 Sơ đồ khối hệ thống', level=2)
    doc.add_paragraph('[Mô tả sơ đồ khối — Chèn ảnh bên dưới]')
    doc.add_paragraph('[<Chèn ảnh sơ đồ khối tại đây>]')
    add_figure_caption(doc, '3.1', 'Sơ đồ khối tổng thể hệ thống')
    
    doc.add_heading('3.2 Sơ đồ nối dây chi tiết', level=2)
    add_table_caption(doc, '3.1', 'Bảng phân công chân GPIO')
    # Bảng GPIO
    gpio_table = doc.add_table(rows=1, cols=4)
    gpio_table.style = 'Table Grid'
    header_cells = gpio_table.rows[0].cells
    header_cells[0].text = 'Linh kiện'
    header_cells[1].text = 'Chân MCU'
    header_cells[2].text = 'Chức năng'
    header_cells[3].text = 'Ghi chú'
    
    doc.add_page_break()
    
    # ===== 12. CHƯƠNG 4 =====
    doc.add_heading('CHƯƠNG 4. THIẾT KẾ PHẦN MỀM', level=1)
    doc.add_heading('4.1 Firmware MCU', level=2)
    doc.add_paragraph('[Mô tả firmware — Thuật toán PID, State Machine, v.v...]')
    
    doc.add_heading('4.2 Tầng giao tiếp', level=2)
    doc.add_paragraph('[ROS2 TF Tree / MQTT / WebSocket...]')
    
    doc.add_heading('4.3 Giao diện ứng dụng', level=2)
    doc.add_paragraph('[Electron+React / Flutter / Web App...]')
    doc.add_page_break()
    
    # ===== 13. CHƯƠNG 5 =====
    doc.add_heading('CHƯƠNG 5. KẾT QUẢ THỰC NGHIỆM', level=1)
    doc.add_heading('5.1 Kết quả chức năng chính', level=2)
    doc.add_paragraph('[Mô tả kết quả đo được, bảng số liệu...]')
    
    doc.add_heading('5.2 Phân tích hiệu năng', level=2)
    add_table_caption(doc, '5.1', 'Bảng tổng hợp kết quả thực nghiệm')
    result_table = doc.add_table(rows=1, cols=3)
    result_table.style = 'Table Grid'
    hdr = result_table.rows[0].cells
    hdr[0].text = 'Chỉ tiêu'; hdr[1].text = 'Kết quả đo được'; hdr[2].text = 'Mục tiêu'
    doc.add_page_break()
    
    # ===== 14. CHƯƠNG 6 =====
    doc.add_heading('CHƯƠNG 6. KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN', level=1)
    doc.add_heading('6.1 Kết luận', level=2)
    doc.add_paragraph('[Tóm tắt những gì đã làm được, kết quả nổi bật...]')
    doc.add_heading('6.2 Hướng phát triển', level=2)
    doc.add_paragraph('[Các hướng nâng cấp, mở rộng trong tương lai...]')
    doc.add_page_break()
    
    # ===== 15. TÀI LIỆU THAM KHẢO =====
    doc.add_heading('TÀI LIỆU THAM KHẢO', level=1)
    refs = [
        'Tác giả A. (Năm). Tên tài liệu. Tên Tạp Chí/NXB.',
        'Open Robotics. (2023). ROS 2 Documentation: Humble Hawksbill. https://docs.ros.org',
    ]
    for ref in refs:
        p = doc.add_paragraph(ref)
        run = p.runs[0]
        run.font.name = 'Times New Roman'
        run.font.size = Pt(12)
    
    doc.add_page_break()
    
    # ===== 16. PHỤ LỤC =====
    doc.add_heading('PHỤ LỤC A: MÃ NGUỒN', level=1)
    doc.add_paragraph('[Dán code quan trọng vào đây — font Courier New 11pt]')
    
    # ===== SAVE =====
    doc.save(file_name)
    print(f'✅ Đã xuất: {file_name}')
    print(f'   Font: Times New Roman 13pt | Lề: 3.5/3.0/3.5/2.0 cm | 1.5 lines')
    print(f'   Số trang: Ở giữa phía trên header (chuẩn TDTU MauDATN_2021)')


# ===== CHẠY =====
if __name__ == '__main__':
    tao_bao_cao_tdtu(
        ten_de_tai   = '[TÊN ĐỀ TÀI CỦA BẠN]',
        sinh_vien    = '[HỌ VÀ TÊN SINH VIÊN]',
        mssv         = '[MÃ SỐ SINH VIÊN]',
        gvhd         = '[TS./ThS. Họ Tên GVHD]',
        chuyen_nganh = '[TÊN KHOA / CHUYÊN NGÀNH]',
        nam          = '2026',
        file_name    = 'BaoCao_TDTU.docx'
    )
```

> ✅ `pip install python-docx pillow requests` trước khi chạy  
> 🔑 Điền thông tin thực tế vào các biến ở phần `if __name__ == '__main__'`  
> 📊 Biểu đồ Mermaid: `npm install -g @mermaid-js/mermaid-cli` (hoặc dùng kroki.io tự động)

### 💡 Quy Tắc Vàng Khi Sinh Biểu Đồ — Dùng Cho Cả Mermaid Lẫn Matplotlib

```python
# ============================================================
# Kích thước CHUẨN khi dùng matplotlib để vẽ chart cho TDTU
# figsize = (width_inch, height_inch)
# 15.5 cm ÷ 2.54 = 6.10 inch → dùng 6.1 x [tùy cao]
# ============================================================
import matplotlib.pyplot as plt

def plot_tdtu_chart(data, title, fig_number, caption, output_path='chart.png'):
    """Vẽ chart matplotlib đúng kích thước trang TDTU, chữ to rõ ràng."""
    fig, ax = plt.subplots(
        figsize=(6.1, 3.8),   # 15.5cm x 9.6cm — vừa vặn 1 trang KHÔNG bị cắt
        dpi=200               # 200 DPI → 1220x760 px → khi thu nhỏ chữ vẫn sắc nét
    )

    # --- Vẽ dữ liệu vào ax ---
    # ax.bar(...)  /  ax.plot(...)  /  ax.pie(...)  tùy loại chart

    ax.set_title(title, fontsize=13, fontweight='bold', pad=10)
    ax.tick_params(labelsize=10)   # Chữ trục đủ to để đọc được sau khi in
    plt.xticks(rotation=30, ha='right')  # Xoay nhãn trục X nếu bị chồng
    plt.tight_layout()             # Tự co để không bị cắt viền
    plt.savefig(output_path, dpi=200, bbox_inches='tight', facecolor='white')
    plt.close()
    return output_path

# Sau khi vẽ xong, chèn vào Word:
# add_image_fitted(doc, 'chart.png')              # tự scale vừa trang
# add_figure_caption(doc, '5.1', 'Tên biểu đồ')  # chú thích bên dưới
```

| Loại biểu đồ | figsize gợi ý | Ghi chú |
|---|---|---|
| Bar/Column chart | `(6.1, 3.8)` | Tỷ lệ 16:10 — đẹp nhất |
| Flowchart/Block diagram | `(6.1, 4.8)` | Hơi cao hơn vì nhiều cấp |
| Scatter/Line plot | `(6.1, 3.5)` | Tỷ lệ ngang, dễ đọc trend |
| Pie chart | `(5.0, 5.0)` | Vuông — pie không méo |
| Biểu đồ phức tạp (nhiều subplot) | `(6.1, 7.0)` | Cho phép `full_page=True` |

> ⚠️ **KHÔNG dùng figsize lớn hơn (8, 6) vì sẽ bị cắt khi chèn vào DOCX. Luôn để `dpi=200` để chữ đủ to.**

---

## 8. Adaptive Behavior (Phản Xạ Thông Minh Theo Context)

| Code quét thấy | AI phản ứng như sau |
|---|---|
| `platformio.ini`, `#include <WiFi.h>`, `digitalWrite`, `servo.write` | **Báo cáo Điện Tử/IoT:** Tập trung Chương 3 (Schematic, GPIO, PWM, I2C) và Chương 4 (Firmware) |
| `react`, `express`, `postgres`, `tailwind` | **Báo cáo Phần Mềm:** Tập trung ERD, Component, REST API, Sequence Diagram xác thực |
| `ros2`, `slam`, `nav2`, `micro_ros` | **Báo cáo Robot/ROS:** Tập trung Kinematics, TF Tree, Costmap, SLAM Toolbox pipeline |
| `tensorflow`, `pandas`, `sklearn` | **Báo cáo AI/ML:** Phương trình mạng neural, Confusion Matrix, Loss curve, Dataset |
| Yêu cầu gấp ("làm liền", "đêm nay") | **Panic Mode:** Ưu tiên 4 mermaid + bảng GPIO + bảng BOM + nội dung chapter 1-3, bỏ qua chứng minh toán phức tạp |

### 📌 Công Thức LaTeX Chuẩn Theo Loại Dự Án

AI PHẢI TỰ SINH các công thức dưới dạng `add_equation(doc, r'$...$', 'X.Y', 'mô tả')`.  
KHÔNG đưa LaTeX dưới dạng text thuần. KHÔNG hỏi user.

#### 🔧 Embedded / IoT (ESP32, STM32, Arduino)
```python
add_equation(doc, r'$T = \frac{1}{f}$', '3.1', 'T: chu kỳ (s), f: tần số (Hz)')
add_equation(doc, r'$Duty = \frac{t_{on}}{T} \times 100\%$', '3.2', 'Duty cycle PWM')
add_equation(doc, r'$P = U \cdot I$', '3.3', 'P: công suất (W), U: điện áp (V), I: dòng điện (A)')
add_equation(doc, r'$\theta_{servo} = \frac{PW - 1000}{1000} \times 180^\circ$', '3.4', 'Góc quay servo từ pulse width')
```

#### 🤖 Robot / ROS2 / AMR (Differential Drive)
```python
add_equation(doc, r'$v = \frac{v_R + v_L}{2}$', '3.1', 'Vận tốc tiến của robot')
add_equation(doc, r'$\omega = \frac{v_R - v_L}{L}$', '3.2', 'Vận tốc góc, L: chiều rộng lưỡng cơ sở')
add_equation(doc, r'$\Delta\phi = \frac{\Delta s_R - \Delta s_L}{L}$', '3.3', 'Bán kính quay')
add_equation(doc, r'$PID = K_p e(t) + K_i\int_0^t e\,d\tau + K_d\dot{e}(t)$', '3.4',
             r'$K_p, K_i, K_d$: hệ số PID; e(t): sai số')
add_equation(doc, r'$v_R = \omega \cdot r$', '3.5', 'Vận tốc bánh địt, r: bán kính bánh')
```

#### 🧠 AI / ML / Deep Learning
```python
add_equation(doc, r'$\hat{y} = \sigma\!\left(W \cdot x + b\right)$', '2.1', 'Output layer sigmoid')
add_equation(doc, r'$L = -\frac{1}{N}\sum_{i=1}^N y_i\log(\hat{y}_i)$', '2.2', 'Hàm mất mát Cross-Entropy')
add_equation(doc, r'$W \leftarrow W - \eta \nabla_W L$', '2.3', 'Gradient Descent, $\eta$: learning rate')
add_equation(doc, r'$\text{IoU} = \frac{|A \cap B|}{|A \cup B|}$', '2.4', 'Độ chính xác vectơ (Object Detection)')
```

#### 💻 Phần Mềm / Web / Hệ Thống
```python
add_equation(doc, r'$t_{RTT} = t_{send} + t_{proc} + t_{recv}$', '4.1', 'Round-trip time hệ thống')
add_equation(doc, r'$T_{hash} = O(1)$', '4.2', 'Độ phức tạp tra cứu JWT cache')
add_equation(doc, r'$QPS = \frac{N_{req}}{\Delta t}$', '4.3', 'Queries per second')
```

> ⚠️ **Quy tắc bắt buộc:**  
> - Luôn dùng `fontsize=16` (mặc định) cho tất cả công thức — đồng đều  
> - Dùng `fontsize=14` nếu công thức có nhiều tầng lồng nhau (`\frac{\frac{a}{b}}{c}`)  
> - `eq_number` theo dạng **Chương.Số**: `'3.1'`, `'3.2'`...  
> - `label` mô tả biến số ngắn gọn: `'v: vận tốc, r: bán kính'`

---

## 8.2 Quy Tắc Tài Liệu Tham Khảo — BẮT BUỘC URL THẬT

> 🚨 **NGHIÊM CẤM**: BẨT BUỘC PHẢI KIỂM TRA URL TRƯỚC KHI ĐƯAT VÀO BÁO CÁO.
> - KHÔNG đưa URL giả hay URL bị 404
> - KHÔNG dùng "(Author, Year)" chung chung không có source
> - KHÔNG trích dẫn phần mềm không có documentation chính thức

### Nguồn Được Phép Sử Dụng

| Loại nguồn | URL đợc chấp nhận | Cách trích dẫn APA |
|---|---|---|
| Repo GitHub chính thức | `github.com/{org}/{repo}` | Author. (Year). *Title*. GitHub. URL |
| Tài liệu chính thức | `docs.ros.org`, `reactjs.org`, `espressif.com` | Org. (Year). *Section*. URL |
| Paper IEEE/arXiv | `ieeexplore.ieee.org/...` `arxiv.org/abs/...` | Author et al. (Year). Title. *Journal*. DOI |
| Sách kỹ thuật ISBN | Google Books / publisher | Author. (Year). *Book Title* (ed.). Publisher |
| Wikipedia (phụ) | `en.wikipedia.org/wiki/...` | Wikipedia. (Year). *Topic*. URL |

### Dịa Sách URL Theo Công Nghệ

```
ROS2:       https://docs.ros.org/en/humble/
MQTT:       https://mqtt.org/mqtt-specification/
ESP-IDF:    https://docs.espressif.com/projects/esp-idf/
PID ctrl:   https://github.com/br3ttb/Arduino-PID-Library
React:      https://react.dev
FastAPI:    https://fastapi.tiangolo.com
SQLite:     https://www.sqlite.org/docs.html
YOLO:       https://github.com/ultralytics/ultralytics
Nav2:       https://navigation.ros.org
OpenCV:     https://docs.opencv.org/
TF Lite:    https://ai.google.dev/edge/litert
python-docx:https://python-docx.readthedocs.io
Mermaid:    https://mermaid.js.org/intro/
```

### Hàm Python Tạo Tham Khảo + Hyperlink Nội Bộ

Chèn vào script sau `add_equation()`:

```python
def add_citation(doc, ref_number: int):
    """
    Chèn trích dẫn nội tuyến dạng [1], [2]... có hyperlink đến phần
    Tài Liệu Tham Khảo cuối báo cáo.

    Ví dụ:
      doc.add_paragraph('MQTT là giao thức nhẹ nhàng ').runs[0]
      add_citation(doc, 3)   # → [3] có link nhảy xuống TLTK số 3
    """
    # Lấy paragraph hiện tại và thêm hyperlink XML
    para = doc.paragraphs[-1]
    # Tạo hyperlink nội bộ (bookmark anchor)
    hyperlink = OxmlElement('w:hyperlink')
    hyperlink.set(qn('w:anchor'), f'ref_{ref_number}')  # trỏ đến bookmark
    rPr_elem = OxmlElement('w:rPr')
    # Màu xanh, gạch chân — trông giống hyperlink
    color = OxmlElement('w:color'); color.set(qn('w:val'), '0563C1')
    u = OxmlElement('w:u'); u.set(qn('w:val'), 'single')
    rPr_elem.append(color); rPr_elem.append(u)
    r_elem = OxmlElement('w:r')
    r_elem.append(rPr_elem)
    t_elem = OxmlElement('w:t')
    t_elem.text = f'[{ref_number}]'
    r_elem.append(t_elem)
    hyperlink.append(r_elem)
    para._p.append(hyperlink)


def add_references_section(doc, references: list):
    """
    Tạo phần Tài Liệu Tham Khảo cuối báo cáo.
    Mỗi mục có Word BOOKMARK để add_citation() có thể nhảy đến.

    references: danh sách dict, mỗi đời mục có:
      {
        'num': 1,
        'apa': 'Macenski, S. et al. (2023). Nav2. GitHub. https://github.com/...',
        'url': 'https://github.com/ros-navigation/navigation2',  # PHẢI THẬT
      }

    AI PHẢI:
    1. Kiểm tra URL trước khi đưa vào list
    2. KHÔNG điền URL placeholder như  'https://example.com'
    3. Nhận xét rõ nếu URL chưa xác nhận được trong chat
    """
    doc.add_heading('TÀI LIỆU THAM KHẢO', level=1)

    for ref in references:
        num = ref['num']
        apa_text = ref['apa']
        url = ref.get('url', '')

        p = doc.add_paragraph()
        p.paragraph_format.left_indent = Cm(1.0)
        p.paragraph_format.first_line_indent = Cm(-1.0)  # Hanging indent APA
        p.paragraph_format.space_after = Pt(6)

        # Thêm BOOKMARK cho mục này (add_citation sẝ dùng)
        bm_start = OxmlElement('w:bookmarkStart')
        bm_start.set(qn('w:id'), str(num))
        bm_start.set(qn('w:name'), f'ref_{num}')
        bm_end = OxmlElement('w:bookmarkEnd')
        bm_end.set(qn('w:id'), str(num))
        p._p.append(bm_start)

        # Số thứ tự
        run_num = p.add_run(f'[{num}] ')
        run_num.font.bold = True
        run_num.font.name = 'Times New Roman'
        run_num.font.size = Pt(12)

        # Nội dung APA
        run_apa = p.add_run(apa_text + ' ')
        run_apa.font.name = 'Times New Roman'
        run_apa.font.size = Pt(12)

        # URL clickable hyperlink (mở trình duyệt)
        if url:
            hyper = OxmlElement('w:hyperlink')
            hyper.set(qn('r:id'),
                doc.part.relate_to(url,
                    'http://schemas.openxmlformats.org/officeDocument/2006/relationships/hyperlink',
                    is_external=True))
            r_url = OxmlElement('w:r')
            rPr_url = OxmlElement('w:rPr')
            color_u = OxmlElement('w:color'); color_u.set(qn('w:val'), '0563C1')
            u_u = OxmlElement('w:u'); u_u.set(qn('w:val'), 'single')
            rPr_url.append(color_u); rPr_url.append(u_u)
            r_url.append(rPr_url)
            t_url = OxmlElement('w:t'); t_url.text = url
            r_url.append(t_url)
            hyper.append(r_url)
            p._p.append(hyper)

        p._p.append(bm_end)


# ============================================================
# VÍ DỤ DÙNG (AI tự thêm URL thật từ dự án thực tế):
# ============================================================
# REFERENCES = [
#     {
#         'num': 1,
#         'apa': 'Macenski, S., Foote, T., Gerkey, B., Lalancette, C., & Woodall, W. (2022). '
#                'Robot Operating System 2: Design, architecture, and uses in the wild. '
#                '*Science Robotics*, 7(66).',
#         'url': 'https://arxiv.org/abs/2211.07752',
#     },
#     {
#         'num': 2,
#         'apa': 'OASIS. (2019). MQTT Version 5.0 Specification. OASIS Standard.',
#         'url': 'https://mqtt.org/mqtt-specification/',
#     },
# ]
# add_references_section(doc, REFERENCES)
```

---

## 9. Checklist Trước Khi Xuất File

Trước khi đưa code Python cho user, AI tự kiểm tra:

- [ ] `file_name` kết thúc bằng `.docx`
- [ ] Lề: `Cm(3.5)` top, `Cm(3.0)` bottom, `Cm(3.5)` left, `Cm(2.0)` right
- [ ] Bìa có **2 trang** + **Logo TDTU** tự tải
- [ ] Font `Times New Roman` 13pt cho Normal
- [ ] Heading 1: IN HOA, Bold, 14pt, Căn giữa, **Page Break Before**
- [ ] Header: Loại đồ án + gạch + số trang | Footer: Tên đề tài + gạch (**Hỏi xác nhận từ user**)
- [ ] Trang trước Chương 1: số **La Mã (i, ii, iii)** | Từ Chương 1: số **Ả Rập (1, 2, 3)**
- [ ] Bảng / ảnh không bị tách trang (`keep_with_next=True`)
- [ ] Có gọi `add_toc(doc)` (Ctrl+A → F9 để update)
- [ ] Chương 4 (ích nhất 5 mục): kiến trúc + firmware + giao tiếp + app + thuật toán
- [ ] Chương 5 có **số liệu đo thực tế** trong bảng (không được điền `??` vào DOCX)
- [ ] Mầu 1.5 đặc tả chức năng (bảng Use Case) được sinh từ source code thực
- [ ] Mỗi mục Chương 2 có **bảng so sánh công nghệ** + kết luận lý do chọn
- [ ] Công thức toán dùng `add_equation()` — **KHÔNG** dán text chữ
- [ ] Đã quét tìm `.png`, `.jpg` dự án và gọi `add_image_fitted()`
- [ ] Biểu đồ dùng `add_mermaid_to_doc()` | Matplotlib `figsize=(6.1, 3.8)` + `dpi=200`
- [ ] Chú thích hình: Bên DƯỚI 12pt Italic | Bảng: Bên TRÊN
- [ ] Tài liệu tham khảo: APA 6th, **mọi URL đã kiểm tra thực tế**, dùng `add_references_section()`
- [ ] Trích dẫn nội tuyến dùng `add_citation(doc, num)` — có hyperlink nhảy xuống TLTK

