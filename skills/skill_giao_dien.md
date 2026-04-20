# 🎨 Premium Cinematic UI Design Skill — v2.0 Pro Edition

> **Version:** 2.0 Pro · **Updated:** 2026-04-19 · **Category:** UI/UX Design  
> **Changelog v2.0:** Added version metadata, cross-skill integration hooks, consistent formatting with skill suite.

> Khi người dùng yêu cầu thiết kế UI/UX cho bất kỳ dự án nào, hãy tuân thủ triệt để mọi kỹ thuật trong file này.

**Cross-skill Integration:**
- Design system tokens → **Snippet Factory** `snip:css-tokens` auto-generates matching CSS variables
- Component hierarchy → **Architecture Planner** validates against blueprint
- UI implementation → **Code Review** checks accessibility (WCAG AA) + performance (animate only transform/opacity)
- Design decisions → **Smart Docs Generator** exports to thesis Chapter 3 (Thiết kế giao diện)
- Design prompt → **Prompt Enhancer** auto-selects `DESIGN_TEMPLATE` with visual direction

---

## 0. Triết lý lõi: "The Ultimate Formula"
Để tạo ra một UI đạt chuẩn "Premium Cinematic", thiết kế bắt buộc phải kết hợp đồng thời 2 lớp giải pháp kỹ thuật sau:
- **Lớp nền tảng (Video 30/60 FPS):** Cắm một file video MP4 hoặc HLS (`z-index: 0`) lặp vô tận. Lớp này chịu trách nhiệm cho các hiệu ứng phức tạp mà trình duyệt không tính toán nổi (như sương mù, gợn nước, ánh sáng không gian thực).
- **Lớp ma thuật tương tác (CSS / Framer Motion 120 FPS):** Các Component giao diện (như thẻ Liquid Glass, chữ Shiny Text) nằm đè lên trên (`z-index: 10+`). Lớp này xử lý độ mượt, tương tác hover, và Scroll-driven parallax dựa trên thao tác cuộn chuột và di chuột của người dùng, mang lại cảm giác "sống động" tuyệt đối.

---

## 1. Tech Stack chuẩn

| Layer | Tool | Ghi chú |
|-------|------|---------|
| Framework | React + Vite + TypeScript | Luôn là lựa chọn mặc định |
| Styling | Tailwind CSS v3/v4 | Design tokens bằng CSS Variables HSL |
| Animation | `framer-motion` (`motion/react`) | Scroll-driven, layout, stagger |
| Video Stream | `hls.js` | Cho `.m3u8` (Mux, Cloudflare Stream) |
| Icons | `lucide-react` | ArrowUpRight, Play, Zap, Palette, BarChart3, Shield, Globe, Menu, X, ChevronDown, Sparkles, Instagram, Twitter, Linkedin, Github, Mail, ArrowRight, Check, Star, Quote, Wand2, BookOpen, Download, Phone |
| UI (tùy chọn) | `shadcn/ui` | Chỉ dùng Button component, phần còn lại tự code |
| Advanced | `gsap` + `ScrollTrigger` | Cho parallax pinning, marquee GSAP |
| 3D (tùy chọn) | `@splinetool/react-spline` | Nhúng scene 3D làm background hero |
| Measure | `react-use-measure` | Cho sizing logic |
| Class merge | `clsx` + `tailwind-merge` | Quản lý class |

---

## 2. Design Tokens & Color Systems

### 2.1 Dark Mode — Cinematic Black (dùng nhiều nhất)
```css
:root {
  --background: 0 0% 0%;        /* Pure black #000000 */
  --foreground: 0 0% 100%;      /* Pure white */
  --card: 0 0% 5%;
  --muted: 0 0% 15%;
  --muted-foreground: 0 0% 65%;
  --border: 0 0% 20%;
  --input: 0 0% 18%;
}
```

### 2.2 Dark Mode — Deep Navy
```css
:root {
  --background: 201 100% 13%;   /* Deep navy blue */
  --background: 260 87% 3%;     /* Deep purple-black */
  --background: 213 45% 67%;    /* Slate blue (cho các biến thể) */
}
```

### 2.3 Dark Mode — Security/Green Accent
```css
:root {
  --background: 0 0% 10%;       /* Dark charcoal */
  --primary: 119 99% 46%;       /* Vivid green */
  --hero-bg: 0 0% 8%;           /* Near black */
}
```

### 2.4 Light Mode — Premium Editorial
```css
/* Background: #FFFFFF hoặc #F8F8F8 */
/* Primary dark text: #051A24, #0D212C */
/* Muted text: #273C46 */
/* Cream accent: #DEDBC8, #E1E0CC */
```

### 2.5 NFT / Web3 — Neon Accent
```css
/* Background: #010828 (deep dark navy) */
/* Text: #EFF4FF (cream) */
/* Accent: #6FFF00 (neon green) */
```

### 2.6 SaaS — Purple/Pink Gradient
```css
/* Background: #010101 */
/* Gradient accent: from-[#FA93FA] via-[#C967E8] to-[#983AD6] */
```

### 2.7 Glass Variables (cho theme có glass)
```css
:root {
  --glass-bg: rgba(255, 255, 255, 0.12);
  --glass-border: rgba(255, 255, 255, 0.25);
  --glass-shadow: 0 4px 30px rgba(0, 0, 0, 0.08);
  --glass-blur: 16px;
}
```

> **Quy tắc**: Tailwind config map tất cả sang `hsl(var(--token))`. Không bao giờ hardcode màu trong component.

---

## 3. Typography — Bảng Font toàn diện

### 3.1 Heading / Display Fonts (Chọn 1)
| Font | Đặc điểm | Dùng cho |
|------|-----------|----------|
| **Instrument Serif** (italic) | Sang trọng, editorial | Hero heading, accent words |
| **Anton** | Bold, uppercase, industrial | NFT, Web3, aggressive branding |
| **PP Mondwest** | Pixel-serif hybrid | Creative studio, editorial |
| **Fustat** (bold) | Modern geometric | SaaS, data products |
| **Sora** | Clean, tech-forward | Security, AI products |
| **General Sans** | Neutral, versatile | Tech recruiting, gradient headings |
| **Rubik** (bold) | Rounded, friendly | Logistics, transport |

### 3.2 Body / UI Fonts (Chọn 1)
| Font | Đặc điểm | Weights |
|------|-----------|---------|
| **Inter** | Tiêu chuẩn vàng | 300, 400, 500, 600, 700 |
| **Barlow** | Hơi hẹp, editorial | 300, 400, 500, 600 |
| **Geist Sans** | Vercel-style | 400, 500, 600, 700 |
| **PP Neue Montreal** | Agency, premium | 400, 500 |
| **Almarai** | Arabic-ready, rounded | 300, 400, 700, 800 |
| **Poppins** | Friendly, geometric | 400, 500, 600 |
| **Manrope** | Modern, compact | 400, 500, 600, 700 |
| **Schibsted Grotesk** | Nordic, clean | 400, 500, 600, 700 |
| **Cabin** | For buttons/tags | 400, 500 |

### 3.3 Accent / Decorative Fonts
| Font | Vai trò |
|------|---------|
| **Condiment** (cursive) | Overlay chữ nghiêng neon lên heading, `mix-blend-exclusion` |
| **Source Serif 4** (italic) | Italic emphasis trong heading |
| `font-mono` (system) | Body text stylized, uppercase |

### 3.4 Quy tắc Typography quan trọng
- **Heading sizing**: `text-5xl sm:text-7xl md:text-8xl` hoặc dùng `clamp()`: `text-[clamp(3rem,8vw,6rem)]`
- **Tracking luôn tight**: `tracking-tight`, `tracking-[-2.46px]`, `tracking-[-4px]`, `-0.04em`, `-0.05em`
- **Leading cực thấp**: `leading-[0.8]`, `leading-[0.85]`, `leading-[0.9]`, `leading-[0.95]`, `leading-none`
- **Color contrast trong heading**: Từ chính màu trắng, từ phụ/italic dùng `text-white/60` hoặc `text-muted-foreground`
- **Superscript trick**: Logo thêm `®` bằng `<sup className="text-xs">®</sup>`
- **Asterisk trick**: Thêm dấu `*` dạng superscript ở cuối chữ cuối: `absolute top-[0.65em] -right-[0.3em] text-[0.31em]`
- **Anti-aliasing bắt buộc**: `-webkit-font-smoothing: antialiased` và `-moz-osx-font-smoothing: grayscale`

---

## 4. Liquid Glass CSS — 3 cấp độ

### 4.1 Liquid Glass Subtle (`.liquid-glass`)
Dùng cho: Navbar pill, Badge, Social icon buttons, Card containers.
```css
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border: none;
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  position: relative;
  overflow: hidden;
}
.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%, rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%, rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%, rgba(255,255,255,0.45) 100%);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

### 4.2 Liquid Glass Strong (`.liquid-glass-strong`)
Dùng cho: CTA buttons, Hero panels, Featured overlays.
```css
.liquid-glass-strong {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(50px);        /* blur MẠNH hơn 12x */
  -webkit-backdrop-filter: blur(50px);
  border: none;
  box-shadow: 4px 4px 4px rgba(0, 0, 0, 0.05),
    inset 0 1px 1px rgba(255, 255, 255, 0.15);
  position: relative;
  overflow: hidden;
}
.liquid-glass-strong::before {
  /* Giống liquid-glass nhưng alpha 0.5/0.2 thay vì 0.45/0.15 */
  ...gradient alpha cao hơn...
}
```

### 4.3 Liquid Glass Dark (biến thể cho light-video backgrounds)
```css
.liquid-glass {
  background: rgba(0, 0, 0, 0.4);  /* Nền đen thay vì trắng */
  /* Gradient border alpha thấp hơn: 0.3/0.1 */
}
```

### 4.4 Consultation Glass (SaaS/Logistics style)
```css
/* backdrop-filter: blur(40px) saturate(180%) */
/* border: 1px solid rgba(255,255,255,0.12) */
/* Diagonal shine gradient chéo trên bề mặt */
/* Inner box-shadow cho depth */
```

> **Nguyên tắc then chốt**: `::before` pseudo-element tạo viền gradient phát sáng mỏng (1.4px) bằng kỹ thuật `mask-composite: exclude`. Viền sáng ở trên/dưới, mờ dần ở giữa.

---

## 5. Video Background — Tất cả kỹ thuật

### 5.0 Auto-Generate Video Background với Hyperframes (AI Driven)
> **Tư duy tối ưu:** Thay vì lên mạng tìm kiếm các đoạn video nền (stock footage) không khớp màu với Brand Color, hãy yêu cầu AI tự lập trình và Generate thẳng ra video 60fps hoàn hảo.
- **Bước 1 (Trong Terminal):** `npx hyperframes init my-bg-video`
- **Bước 2 (Prompt AI):** "Viết file HTML dùng thư viện GSAP/Lottie tạo một hiệu ứng background [lưới sương mù / ánh sáng cực quang / hạt phân tử] mượt mà dài 10 giây chuẩn màu [mã Hex màu] bằng Hyperframes"
- **Bước 3 (Trong Terminal):** `npx hyperframes render` (Xuất thẳng ra file `.mp4` nhờ FFmpeg)
- **Bước 4 (Trong Code):** Lắp file video vừa sinh ra vào thẻ `<video>` ở mục 5.1 bên dưới cùng `mix-blend-mode` siêu đẹp.

### 5.1 Video MP4 đơn giản (phổ biến nhất)
```jsx
<video
  autoPlay loop muted playsInline
  className="absolute inset-0 w-full h-full object-cover z-0"
>
  <source src="URL.mp4" type="video/mp4" />
</video>
```

### 5.2 Video HLS streaming (qua hls.js)
```js
import Hls from 'hls.js';

useEffect(() => {
  const video = videoRef.current;
  if (Hls.isSupported()) {
    const hls = new Hls({ enableWorker: false });
    hls.loadSource('URL.m3u8');
    hls.attachMedia(video);
  } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
    video.src = 'URL.m3u8'; // Safari native HLS
  }
  return () => hls?.destroy();
}, []);
```

### 5.3 Custom JS Fade Loop (tạo loop mượt không flash)
```js
// On canplay: fade opacity 0 → 1 over 500ms via requestAnimationFrame
// On timeupdate: khi remaining ≤ 0.55s → fade opacity → 0 over 500ms
// On ended: set opacity=0, wait 100ms, reset currentTime=0, play(), fade to 1
// fadingOutRef boolean ngăn re-trigger fade-out bởi repeated timeUpdate
// Mỗi fade mới cancel running animation frame trước đó
// Fade resume từ opacity hiện tại (không snap)
```

### 5.4 Gradient Overlays trên video
```
- Top fade: h-[200px] bg-gradient-to-b from-black to-transparent
- Bottom fade: h-[200px-300px] bg-gradient-to-t from-black to-transparent
- Dark overlay: bg-black/5 (nhẹ) đến bg-black/60 (nặng)
- pointer-events-none trên tất cả overlay
```

### 5.5 Desaturated Video
```css
/* Stats section: filter: saturate(0) cho video B&W */
```

### 5.6 Video blend mode
```css
/* mix-blend-screen: video nền đen biến mất, chỉ hiện phần sáng */
/* Dùng cho Spline 3D hoặc Glassy Orb */
```

### 5.7 Noise/Texture Overlay trên video
```css
.noise-overlay {
  /* Inline SVG data URI với feTurbulence filter */
  /* baseFrequency: 0.85, numOctaves: 3 */
  /* opacity-[0.7] mix-blend-overlay pointer-events-none */
}
```

### 5.8 Full-screen fixed texture layer
```
/* z-50 pointer-events-none fixed inset-0 */
/* /texture.png với mix-blend-mode: lighten, opacity: 0.6 */
/* background-size: cover */
```

---

## 6. Navbar — Tất cả biến thể

### 6.1 Floating Glass Pill (phổ biến nhất)
```
fixed top-0 (hoặc top-4) left-0 right-0 z-50
Inner: inline-flex items-center rounded-full backdrop-blur-md
       border border-white/10 bg-surface px-2 py-2
Shadow khi scroll: shadow-md shadow-black/10 khi scrollY > 100
```
- Logo trái: Icon/text + divider `w-px h-5 bg-stroke`
- Links giữa: `text-xs sm:text-sm rounded-full px-3 py-1.5`
- CTA phải: Glass pill hoặc solid button

### 6.2 Black Hanging Pill (Prisma style)
```
Absolutely positioned ở top center
bg-black rounded-b-2xl md:rounded-b-3xl px-4 py-2 md:px-8
/* Treo từ mép trên xuống, bo tròn chỉ ở dưới */
```

### 6.3 Full-width Transparent (Classic)
```
fixed top-0 w-full z-50, py-5 px-8, flex justify-between
/* Không có background, hoàn toàn trong suốt */
/* Gradient divider bên dưới: h-px bg-gradient-to-r from-transparent via-foreground/20 to-transparent */
```

### 6.4 Solid Glass Bar (VEX style)
```
rounded-xl px-4 py-2 liquid-glass
/* Bọc toàn bộ navbar trong 1 khối glass bo tròn */
```

### 6.5 Mobile Menu
```
Hamburger icon (Menu/X from lucide-react)
Toggle full-screen overlay: bg-white/95 backdrop-blur rounded shadow
Hoặc full-screen bg-black overlay menu
```

---

## 7. Hero Section — Tất cả layout patterns

### 7.1 Centered Cinematic (phổ biến nhất)
```
min-h-screen flex flex-col items-center justify-center text-center
px-6 pt-32 pb-40
/* Video nền absolute inset-0 */
/* Badge pill → Heading → Subtext → CTA buttons */
```

### 7.2 Bottom-left Aligned
```
min-h-screen flex items-end
/* Content ở góc dưới-trái */
/* pb-10 md:pb-10 pt-32 */
/* max-w-2xl text-left */
```

### 7.3 Bottom Split (2 columns)
```
flex-1 flex flex-col justify-end pb-12 lg:pb-16
lg:grid lg:grid-cols-2 lg:items-end
/* Left: heading + buttons */
/* Right: glass tag card aligned bottom-right */
```

### 7.4 Left-aligned Hero (8-col / 4-col grid)
```
12-column grid: left 8 columns cho heading
right 4 columns cho text + CTA button
/* Giant display text spanning 8 cols */
```

### 7.5 Two-Panel Split (Bloom style)
```
flex row min-h-screen
Left panel: w-[52%] liquid-glass-strong overlay
Right panel: w-[48%] (hidden on mobile lg:flex)
/* Left = content, Right = feature cards */
```

### 7.6 Top-aligned Hero (không center)
```
pt-32 md:pt-48 /* Push content lên trên */
/* Không dùng justify-center, dùng padding-top lớn */
```

---

## 8. Badge / Pill Patterns

### 8.1 Glass Badge with inner "New" tag
```jsx
<div className="liquid-glass rounded-full px-1 py-1 inline-flex items-center gap-2">
  <span className="bg-white text-black rounded-full px-3 py-1 text-xs font-semibold">New</span>
  <span className="text-sm text-muted-foreground">Introducing AI-powered design.</span>
</div>
```

### 8.2 Simple Glass Badge
```jsx
<div className="liquid-glass rounded-full px-3.5 py-1">
  <span className="text-xs font-medium text-white">How It Works</span>
</div>
```

### 8.3 Bordered Pill Badge
```jsx
<div className="rounded-full border border-white/20 backdrop-blur-sm px-4 py-1.5 inline-flex items-center gap-1.5">
  <Sparkles className="w-3 h-3 text-white/80" />
  <span className="text-sm font-medium text-white/80">New AI Automation Ally</span>
</div>
```

### 8.4 Dark Badge with Date
```jsx
/* rounded-[20px], bg-white/10, border border-white/20 */
/* Dot 4px white + text white/60 + bold date text white */
```

### 8.5 "Featured in X" Liquid Glass Badge
```
/* Outer ring: liquid-glass (white/10, backdrop-blur-sm) */
/* Inner pill: white/90 backdrop-blur-md */
```

---

## 9. Animation Patterns — Tham chiếu đầy đủ

### 9.1 BlurText Component (Word-by-word blur reveal)
```js
// Splits text by words hoặc characters
// IntersectionObserver trigger on scroll
// Mỗi word = <motion.span> animate:
//   from: { filter: 'blur(10px)', opacity: 0, y: 50 }
//   mid:  { filter: 'blur(5px)',  opacity: 0.5, y: -5 }
//   to:   { filter: 'blur(0px)',  opacity: 1, y: 0 }
// Stagger: 200ms between elements
// Step duration: 0.35s mỗi keyframe step
```

### 9.2 AnimatedHeading (Character-by-character slide)
```js
// Split text by \n thành lines, mỗi line thành characters
// Mỗi char = <span> inline-block với CSS transitions
// from: opacity: 0, translateX(-18px)
// to:   opacity: 1, translateX(0)
// Delay mỗi char: (lineIndex * lineLength * charDelay) + (charIndex * charDelay)
// charDelay = 30ms, initialDelay = 200ms
// Transition duration: 500ms mỗi character
// Spaces render as \u00A0 (non-breaking space)
```

### 9.3 WordsPullUp (Pull-up with stagger)
```js
// Splits text by spaces
// Mỗi word = motion.span slides up (y: 20 → 0)
// useInView (once: true)
// Stagger delay: 0.08s between words
// Supports showAsterisk prop: * superscript cuối từ cuối
```

### 9.4 WordsPullUpMultiStyle (Multi-segment styled pull-up)
```js
// Array of { text, className } segments
// Mỗi word giữ className riêng (normal vs italic vs muted)
// Same pull-up animation, inline-flex flex-wrap
```

### 9.5 Scroll-Driven Character Opacity (AnimatedLetter)
```js
// Mỗi character bọc trong AnimatedLetter component
// useScroll({ target, offset: ['start 0.8', 'end 0.2'] })
// Opacity map: 0.2 → 1 based on scroll progress
// charProgress = index / totalChars
// Range: [charProgress - 0.1, charProgress + 0.05]
// Tạo hiệu ứng từng chữ sáng dần khi cuộn
```

### 9.6 Scroll-Driven Word Reveal (Testimonial style)
```js
// useScroll({ target: containerRef, offset: ["start end", "end center"] })
// Mỗi word = <motion.span> với mr-[0.3em]
// Word[i] map range [i/total, (i+1)/total] → opacity [0.2, 1]
// Cộng thêm color transition: "hsl(0 0% 35%)" → "hsl(0 0% 100%)"
```

### 9.7 Staggered FadeUp (Framer Motion helper)
```js
const fadeUp = (delay) => ({
  initial: { opacity: 0, y: 20 },
  whileInView: { opacity: 1, y: 0 },
  viewport: { once: true, margin: "-100px" },
  transition: { duration: 0.6, delay, ease: "easeOut" },
});
// Dùng: <motion.div {...fadeUp(0.1)} />
```

### 9.8 CSS Fade-Rise (Pure CSS, không cần Framer)
```css
@keyframes fade-rise {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-fade-rise        { animation: fade-rise 0.8s ease-out both; }
.animate-fade-rise-delay  { animation: fade-rise 0.8s ease-out 0.2s both; }
.animate-fade-rise-delay-2{ animation: fade-rise 0.8s ease-out 0.4s both; }
```

### 9.9 CSS FadeUp with Blur (Premium feel)
```css
@keyframes fade-up {
  0%   { opacity: 0; transform: translateY(20px); filter: blur(4px); }
  100% { opacity: 1; transform: translateY(0);    filter: blur(0); }
}
.animate-fade-up { animation: fade-up 0.7s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
/* Dùng kết hợp opacity-0 và style={{ animationDelay: "0.2s" }} cho stagger */
```

### 9.10 FadeIn Wrapper Component (Pure React, no Framer)
```js
// setTimeout + React state → opacity: 0 to 1
// Configurable delay (ms) và duration (ms)
// Uses inline transitionDuration + Tailwind's transition-opacity
```

### 9.11 GSAP Entrance Timeline
```js
// gsap.timeline({ ease: "power3.out" })
// .name-reveal: opacity 0→1, y 50→0, duration 1.2s, delay 0.1s
// .blur-in: opacity 0→1, filter blur(10px)→blur(0px), y 20→0, stagger 0.1, delay 0.3s
```

### 9.12 GSAP Marquee
```js
// "TEXT • " repeated 10x
// gsap xPercent: -50, duration 40, ease "none", repeat -1
```

### 9.13 Card Entrance (Scale + Fade)
```js
// scale from 0.95 + opacity 0 → 1
// useInView (once: true, margin "-100px")
// Stagger 0.15s per card
// ease: [0.22, 1, 0.36, 1]
```

### 9.14 CSS Infinite Marquee
```css
@keyframes marquee {
  0%   { transform: translateX(0%); }
  100% { transform: translateX(-50%); }
}
.animate-marquee { animation: marquee 20s linear infinite; }
/* Desktop 30s, Mobile 10s */
/* Images/logos duplicated 2x for seamless loop */
```

### 9.15 Scroll Indicator
```css
@keyframes scroll-down {
  from { transform: translateY(-100%); }
  to   { transform: translateY(200%); }
}
/* w-px h-10 bg-stroke line with animated highlight */
/* Label: "SCROLL" text-xs text-muted uppercase tracking-[0.2em] */
```

### 9.16 Role Cycling Text
```js
// Roles: ["Creative", "Fullstack", "Founder", "Scholar"]
// Cycle every 2s with key={roleIndex} for re-trigger
// animate-role-fade-in: opacity 0 + translateY(8px) → opacity 1 + translateY(0)
```

### 9.17 Gradient Shift Animation (Border glow)
```css
@keyframes gradient-shift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
/* 6s ease infinite, cho animated gradient borders */
```

### 9.18 Loading Screen Pattern
```
- Full spinner: fixed inset-0 z-[9999] bg-bg
- Top-left: "Portfolio" label, text-xs text-muted uppercase tracking-[0.3em]
- Center: Rotating words ["Design", "Create", "Inspire"] cycling every 900ms
  AnimatePresence mode="wait", y:20→0→-20
- Bottom-right: Counter 000→100 over 2700ms via requestAnimationFrame
  text-6xl md:text-8xl lg:text-9xl font-display tabular-nums
- Bottom: 3px progress bar h-[3px] bg-stroke/50
  Fill: accent-gradient, scaleX(progress/100)
- On 100: 400ms delay → onComplete()
```

---

## 10. Section Layout Patterns

### 10.1 Features Chess (Zigzag)
```
Row 1: flex → content LEFT / image RIGHT
Row 2: flex-row-reverse → content RIGHT / image LEFT
/* GIF/video trong liquid-glass rounded-2xl overflow-hidden */
```

### 10.2 Features Grid (4 cards)
```
grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6
Mỗi card: liquid-glass rounded-2xl p-6
Icon: liquid-glass-strong rounded-full w-10 h-10
```

### 10.3 Stats Section
```
HLS video background (desaturated: filter: saturate(0))
liquid-glass rounded-3xl p-12 md:p-16 card
4-column grid: "200+" / "Sites launched" etc.
Values: text-4xl md:text-5xl lg:text-6xl font-heading italic
Labels: text-white/60 font-body font-light text-sm
```

### 10.4 Testimonials (3-column grid)
```
md:grid-cols-3 gap-6
Card: liquid-glass rounded-2xl p-8
Quote: text-white/80 font-light text-sm italic
Name: text-white font-medium text-sm
Role: text-white/50 font-light text-xs
```

### 10.5 Testimonial Carousel (Auto-scrolling)
```
3s interval, pauses on hover
Prev/next: w-12 h-12 rounded-full border border-[#0D212C]/20
Cards: 427.5px wide desktop, rounded-[32px] md:rounded-[40px]
Shadow: 0_4px_16px_rgba(0,0,0,0.08)
Transform: cubic-bezier(0.4, 0, 0.2, 1) 0.8s transition
Tripled array for infinite scroll
```

### 10.6 NFT Card Grid
```
3-column grid lg:grid-cols-3, gap 24px
Card: liquid-glass rounded-[32px] p-[18px] hover:bg-white/10
Video: square aspect-ratio (pb-[100%] trick) rounded-[24px]
Overlay bar: liquid-glass rounded-[20px] px-5 py-4
Purple gradient action button: bg-gradient-to-br from-[#b724ff] to-[#7c3aed]
shadow-lg shadow-purple-500/50, hover:scale-110
```

### 10.7 Services Cards (Video + Content)
```
liquid-glass rounded-3xl overflow-hidden with group class
Video area: aspect-video object-cover
group-hover:scale-105 transition-transform duration-700
Gradient: bg-gradient-to-t from-black/40 to-transparent
Body: tag label (uppercase tracking-widest text-white/40 text-xs)
      + ArrowUpRight in liquid-glass circle
      + title + description
```

### 10.8 Bento Grid (Portfolio)
```
grid-cols-1 md:grid-cols-12 gap-5 md:gap-6
Column spans alternate: 7/5/5/7
Halftone overlay: radial-gradient(circle, #000 1px, transparent 1px) 4×4px
Hover: backdrop-blur-lg + label pill with animated gradient border
```

### 10.9 Partner Section (Mouse Trail)
```
Large white container py-48 rounded-[40px]
On hover: GIF thumbnails spawn at cursor position
Random rotation (-10 to +10 deg)
Fade out 1000ms with scale-down
Spawn throttle: 80ms minimum
```

### 10.10 Parallax Gallery (GSAP)
```
min-h-[300vh] section
Layer 1: Pinned center (GSAP ScrollTrigger.create pin)
Layer 2: 2-column parallax grid
Cards: aspect-square max-w-[320px] with rotation
Lightbox on click
```

### 10.11 Journal Entries
```
Horizontal pills rounded-[40px] sm:rounded-full
flex items-center gap-6 p-4 bg-surface/30 hover:bg-surface
Title, image, read time, date
```

---

## 11. Button Patterns

### 11.1 Liquid Glass CTA
```
liquid-glass-strong rounded-full px-5 py-2.5
text-foreground text-sm font-medium
ArrowUpRight icon bên phải
hover:scale-[1.03] hover:bg-white/5
whileHover={{ scale: 1.05 }} whileTap={{ scale: 0.95 }}
```

### 11.2 Solid White CTA
```
bg-white text-black rounded-full px-6 py-3 font-medium
hover:bg-gray-100
```

### 11.3 Pill with Circle Icon (Prisma style)
```
bg-primary rounded-full flex items-center gap-2
Text left + Circle (bg-black rounded-full w-9 h-9) right chứa ArrowRight icon
Hover: gap tăng (hover:gap-3), circle scale (group-hover:scale-110)
```

### 11.4 Glow Button (SaaS/ClearInvoice)
```
bg-gradient-to-r from-[#FF3300] to-[#EE7926]
Absolute glow div behind: bg-orange-600 blur-lg opacity-20
Inner stroke: 1.5px border-white/20 overlay
Hover: scale 1.05, glow opacity-60, Arrow slides in
```

### 11.5 Clip-Path Geometric (Targo)
```
clip-path: polygon vát chéo 10-12px ở top-right và bottom-left
bg-[#EE3F2C] text-white (hoặc bg-white text-dark)
```

### 11.6 Hero Secondary (Gradient border hover)
```
liquid-glass text-foreground rounded-full
Hover: absolute span inset: -2px with accent gradient behind
Inner content: bg-surface rounded-full backdrop-blur-md
```

### 11.7 Multi-Layer Shadow Button (Viktor Oddy)
```
box-shadow: 
  0_1px_2px_0_rgba(5,26,36,0.1),
  0_4px_4px_0_rgba(5,26,36,0.09),
  0_9px_6px_0_rgba(5,26,36,0.05),
  0_17px_7px_0_rgba(5,26,36,0.01),
  0_26px_7px_0_rgba(5,26,36,0),
  inset_0_2px_8px_0_rgba(255,255,255,0.5)
```

### 11.8 SVG Path Custom Shape Button
```
184px x 65px container
Inner: SVG absolute inset-0 with custom path filled white
Text centered on top: Rubik Bold Uppercase 20px #161a20
hover:scale-105, active:scale-95
```

### 11.9 Waitlist Glow Button (Web3)
```
Outer: 0.6px solid white border pill
Inner: black bg pill, text white 14px font-medium, px-29 py-11
Top glow: blurred white-to-transparent gradient blob
```

---

## 12. Special Techniques

### 12.1 Cursive Overlay (Condiment style)
```
Font: Condiment (cursive), neon green (#6FFF00)
positioned absolute, slightly rotated: -rotate-1
mix-blend-exclusion, opacity-90
Placed overlapping heading text ở góc bottom-right
```

### 12.2 Gradient Text
```css
background-image: linear-gradient(to right, #fff, #6366f1, #a855f7, #fcd34d);
/* hoặc: linear-gradient(223deg, #E8E8E9 0%, #3A7BBF 104.15%) */
background-clip: text;
-webkit-background-clip: text;
color: transparent;
```

### 12.3 ShinyText Component (Animated shimmer)
```
Base color: #64CEFB
Shine color: #ffffff
Gradient sweeps 100deg, 3s animation speed
backgroundClip: text, color: transparent
Continuous left-to-right using framer-motion
```

### 12.4 Coded Dashboard Mockup (không dùng ảnh)
```
Frosted glass wrapper: rounded-2xl p-3 md:p-4
background: rgba(255,255,255,0.4), border: 1px solid rgba(255,255,255,0.5)
boxShadow: var(--shadow-dashboard) = 0 25px 80px -12px rgba(0,0,0,0.08)
Dashboard bên trong: text-[11px] select-none pointer-events-none
Top bar, Sidebar w-40, Main content with SVG chart
SVG area chart: hand-crafted cubic Bézier path, gradient fill
```

### 12.5 Parallax Dashboard Image
```
Framer Motion useScroll + useTransform
y: [0, -250] parallax scroll offset
mixBlendMode: "luminosity"
rounded-2xl shadow, max-w-5xl w-[90%]
```

### 12.6 Corner Accents
```
4 div 7px x 7px solid white
positioned absolute tại 4 góc của hero content container
```

### 12.7 Grid Lines Background
```
3 thin vertical lines (white/10 opacity)
tại marks 25%, 50%, 75% screen width
visible desktop only
```

### 12.8 Central Glow SVG
```
Large horizontal SVG ellipse tại center-top
Cyan/dark green hue, 25px Gaussian blur filter
```

### 12.9 Inset Hero (Prisma)
```
h-screen section with p-4 md:p-6 padding
/* Tạo viền đen bao quanh video */
Inner container: rounded-2xl md:rounded-[2rem] overflow-hidden
```

### 12.10 Accent Gradient (Portfolio)
```css
.accent-gradient {
  background: linear-gradient(90deg, #89AACC 0%, #4E85BF 100%);
}
/* Dùng cho: logo ring, hover borders, progress bars */
```

### 12.11 Decorative Ghost Text
```
Text opacity-10 (nearly invisible)
Monospace uppercase, same content repeated
Decorative filler, 2 columns
Mobile: text-[#010828] invisible against dark bg
```

### 12.12 Subtle Radial Gradient Background
```
bg-[radial-gradient(ellipse_at_top,_rgba(255,255,255,0.03)_0%,_transparent_70%)]
bg-[radial-gradient(ellipse_at_center,_rgba(255,255,255,0.02)_0%,_transparent_60%)]
/* Rất nhẹ, tạo depth cho sections trên nền đen */
```

### 12.13 Blurred Overlay Shape
```
w-[984px] h-[527px] opacity-90 bg-gray-950 blur-[82px]
absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2
pointer-events-none
/* Blob mờ đặt sau hero text để nổi chữ */
```

### 12.14 Video Color Filter (Glassy Orb)
```css
filter: hue-rotate(-55deg) saturate(250%) brightness(1.2) contrast(1.1);
/* Transform purple asset → Electric Blue */
mix-blend-screen;
transform: scale(1.25);
```

### 12.15 Top Gradient Bar (SaaS)
```
h-[5px] w-full
bg-gradient-to-r from-[#ccf] via-[#e7d04c] to-[#31fb78]
/* Dải đầy màu sắc ở đỉnh trang */
```

### 12.16 Tab Auto-Cycling
```js
// 4 tabs auto-cycle every 4s via setInterval
// useState('analyse')
// Active: bg-white text-black shadow-sm
// Inactive: text-gray-600
// Overlay content animated per tab
```

---

## 13. Footer Patterns

### 13.1 Minimal (border-t)
```
mt-32 pt-8 border-t border-white/10
Left: "© 2026 Studio. All rights reserved." text-white/40 text-xs
Right: Privacy, Terms, Contact links text-white/40 text-xs
```

### 13.2 Fixed Bottom Nav (Floating pill)
```
fixed bottom-6 left-1/2 -translate-x-1/2 z-50
bg-white rounded-full px-8 py-2
Complex layered shadow
"V" letter + "Start a chat" CTA
```

### 13.3 Full Footer with Columns
```
py-12 px-8 md:px-28
Left: CTA button
Right: ArrowUpRight icon + 2 columns of links
```

### 13.4 GSAP Marquee Footer
```
"BUILDING THE FUTURE • " repeated 10x
gsap xPercent: -50, duration 40, repeat -1
Social links + Green pulsing dot + "Available for projects"
```

---

## 14. Responsive Strategy

### 14.1 Breakpoints tiêu chuẩn
```
sm: 640px, md: 768px, lg: 1024px, xl: 1280px, 2xl: 1536px
```

### 14.2 Content Max-Width
```
max-w-7xl (1280px) — phổ biến nhất
max-w-6xl (1152px) — cho full-page content sites
max-w-5xl (1024px) — cho centered hero/navbar
max-w-[1200px] — projects/footer
max-w-[1831px] — extra-wide layouts (NFT)
max-w-[1400px] — parallax galleries
```

### 14.3 Mobile Patterns
```
- Navbar links: hidden md:flex hoặc hidden lg:flex
- Hamburger menu xuất hiện ở mobile
- Grid: 1-col mobile → 2-col md → 3-4 col lg
- Font sizes scale: text-4xl → text-5xl md → text-6xl lg → text-7xl xl
- Padding giảm: px-6 mobile → px-8 md → px-12 lg → px-16 xl
- Hero heading dùng vw units: text-[26vw] → text-[19vw]
```

---

## 15. File Structure chuẩn

```
src/
├── index.css           (CSS variables, liquid-glass, animations, font imports)
├── App.tsx             (Layout + Router)
├── pages/
│   └── Index.tsx       (Main page composition)
├── components/
│   ├── Navbar.tsx
│   ├── Hero.tsx
│   ├── AboutSection.tsx
│   ├── FeaturedVideoSection.tsx
│   ├── FeaturesChess.tsx
│   ├── FeaturesGrid.tsx
│   ├── Stats.tsx
│   ├── Testimonials.tsx
│   ├── TestimonialCarousel.tsx
│   ├── ServicesSection.tsx
│   ├── ProjectsSection.tsx
│   ├── PricingSection.tsx
│   ├── PartnerSection.tsx
│   ├── CtaFooter.tsx
│   ├── Footer.tsx
│   ├── BottomNav.tsx
│   ├── LoadingScreen.tsx
│   ├── BlurText.tsx          (Custom word-by-word animated text)
│   ├── AnimatedHeading.tsx   (Character-by-character slide)
│   ├── WordsPullUp.tsx       (Pull-up stagger)
│   ├── ShinyText.tsx         (Gradient shimmer text)
│   ├── FadeIn.tsx            (Generic fade wrapper)
│   ├── VideoBackground.tsx   (HLS/MP4 + fade logic)
│   └── ui/
│       ├── button.tsx        (shadcn button with hero variants)
│       └── infinite-slider.tsx
├── hooks/
│   └── useInViewAnimation.ts (IntersectionObserver hook)
├── assets/
│   ├── logo.png / logo-icon.png
│   ├── feature-1.gif, feature-2.gif
│   ├── hero-dashboard.png
│   └── avatars/
└── styles/
    ├── fonts.css
    └── theme.css
```

---

## 16. Checklist khi áp dụng Skill

- [ ] Chọn Color theme phù hợp (Dark/Light/NFT/SaaS)
- [ ] Chọn 1 Display font + 1 Body font từ bảng trên
- [ ] Thêm `.liquid-glass` CSS vào `index.css`
- [ ] Video background với `autoPlay loop muted playsInline`
- [ ] Gradient overlays trên video (top + bottom fade)
- [ ] Navbar dạng floating glass pill
- [ ] Hero heading với Blur-in hoặc Pull-up animation
- [ ] Badge pill ở trên heading
- [ ] CTA button glass hoặc solid white
- [ ] Staggered entrance animations (delay 0.1s → 0.2s → 0.3s)
- [ ] Anti-aliasing fonts
- [ ] Responsive breakpoints mobile-first
- [ ] `pointer-events-none` trên mọi overlay decorative
- [ ] `object-cover` trên mọi video/image
- [ ] Design tokens dùng CSS Variables HSL, map qua Tailwind config
