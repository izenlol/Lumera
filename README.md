
<html lang="en" dir="ltr" data-theme="light">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Luméra — Hair Care</title>
<meta name="description" content="Luméra — radiant hair care. Oil, detangler and cream, made to catch the light.">
<!-- ============================================================
     LUMÉRA v3 — bilingual (EN/AR) single-file storefront
     • Colors  → CSS variables in :root (synced to logo gradient)
     • Products→ PRODUCTS array in the script block (en + ar fields)
     • Text    → I18N dictionary in the script block
     ============================================================ -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@600;700;800&family=Rubik:ital,wght@0,400;0,500;0,600;1,400&family=Changa:wght@600;700;800&display=swap" rel="stylesheet">
<style>
/* ============ TOKENS — synced to the Luméra logo ============ */
:root{
  --g1:#FF3D9A; --g2:#FF7E6B; --g3:#FFB25C; --g4:#FFD84D;
  --grad:linear-gradient(100deg,var(--g1) 0%,var(--g2) 36%,var(--g3) 66%,var(--g4) 100%);
  --grad-soft:linear-gradient(115deg,#FFE3F0 0%,#FFE9DD 45%,#FFF4D6 100%);
  --bg:#FFF7F4;
  --surface:#FFFFFF;
  --ink:#42202F;
  --muted:#9A7484;
  --line:#F3DFDC;
  --shadow:0 24px 48px -24px rgba(66,32,47,.22);
  --radius:20px;
  --font-display:'Syne',sans-serif;
  --font-body:'Rubik',sans-serif;
  --nav-h:68px;
  --bar-h:38px;
}
[data-theme="dark"]{
  --bg:#221019;
  --surface:#2C1620;
  --ink:#FFEFF2;
  --muted:#C79AA8;
  --line:#42222F;
  --shadow:0 24px 48px -24px rgba(0,0,0,.5);
  --grad-soft:linear-gradient(115deg,#4A2138 0%,#4A2B22 45%,#4A3B1C 100%);
}
[lang="ar"] body,[lang="ar"] button,[lang="ar"] input,[lang="ar"] textarea{font-family:'Rubik','Changa',sans-serif}
[lang="ar"] h1,[lang="ar"] h2,[lang="ar"] h3,[lang="ar"] h4,[lang="ar"] .card-name{font-family:'Changa',sans-serif;letter-spacing:0}
[lang="ar"] .eyebrow{letter-spacing:.04em}

*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth;scroll-padding-top:calc(var(--nav-h) + var(--bar-h) + 12px)}
@media (prefers-reduced-motion:reduce){
  html{scroll-behavior:auto}
  *,*::before,*::after{animation-duration:.001s!important;transition-duration:.001s!important}
}
body{
  background:var(--bg);color:var(--ink);
  font-family:var(--font-body);font-size:16px;line-height:1.65;
  -webkit-font-smoothing:antialiased;
  transition:background .3s,color .3s;
}
body.locked{overflow:hidden}
::selection{background:var(--g1);color:#fff}
a{color:inherit}
button{font-family:inherit;cursor:pointer;color:inherit}
:focus-visible{outline:2px solid var(--g1);outline-offset:3px;border-radius:4px}

.wrap{max-width:1060px;margin:0 auto;padding:0 24px}
.eyebrow{
  font-size:12px;letter-spacing:.18em;text-transform:uppercase;
  color:var(--muted);font-weight:600;display:flex;align-items:center;gap:10px;
}
.eyebrow::before{content:"";width:26px;height:2px;background:var(--grad);border-radius:2px;display:inline-block}
h1,h2,h3{font-family:var(--font-display);line-height:1.12;letter-spacing:-.015em;text-wrap:balance}
.wordmark{
  font-family:var(--font-display);font-weight:800;font-style:italic;
  font-size:20px;letter-spacing:.03em;text-transform:uppercase;
  background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent;
  text-decoration:none;transform:skewX(-4deg);display:inline-block;
}

/* ============ ANNOUNCEMENT BAR ============ */
.announce{
  position:fixed;top:0;left:0;right:0;z-index:65;height:var(--bar-h);
  background:var(--grad);color:#fff;display:flex;align-items:center;justify-content:center;
  font-size:13px;font-weight:600;gap:14px;padding:0 44px;text-align:center;
  transition:transform .3s;
}
.announce.hidden{transform:translateY(-100%)}
.announce button{
  position:absolute;inset-inline-end:10px;background:none;border:none;color:#fff;
  font-size:18px;line-height:1;padding:6px;opacity:.85;
}
.announce button:hover{opacity:1}
body.announce-on .nav{top:var(--bar-h)}
body.announce-on{--announce-offset:var(--bar-h)}
body:not(.announce-on){--announce-offset:0px}

/* scroll progress */
.progress{
  position:fixed;top:calc(var(--nav-h) + var(--announce-offset));left:0;height:2.5px;width:0;
  background:var(--grad);z-index:61;transition:width .1s linear;border-radius:0 3px 3px 0;
}
[dir="rtl"] .progress{left:auto;right:0;border-radius:3px 0 0 3px}

/* ============ NAV ============ */
.nav{
  position:fixed;top:0;left:0;right:0;z-index:60;height:var(--nav-h);display:flex;align-items:center;
  background:color-mix(in srgb,var(--bg) 84%,transparent);
  backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);
  border-bottom:1px solid transparent;transition:border-color .3s,background .3s,top .3s;
}
.nav.scrolled{border-bottom-color:var(--line)}
.nav-inner{width:100%;max-width:1060px;margin:0 auto;padding:0 24px;display:flex;align-items:center;justify-content:space-between;gap:20px}
.nav-links{display:flex;gap:6px;list-style:none}
.nav-links a{
  text-decoration:none;font-size:14px;font-weight:500;color:var(--muted);
  padding:8px 14px;border-radius:100px;transition:color .2s,background .2s;
}
.nav-links a:hover{color:var(--ink)}
.nav-links a.active{color:var(--ink);background:var(--grad-soft)}
.nav-actions{display:flex;align-items:center;gap:10px}
.icon-btn{
  width:42px;height:42px;border-radius:50%;border:1.5px solid var(--line);background:var(--surface);
  display:flex;align-items:center;justify-content:center;transition:border-color .2s,transform .2s;flex-shrink:0;
}
.icon-btn:hover{border-color:var(--g1);transform:translateY(-1px)}
.icon-btn:active{transform:scale(.94)}
.icon-btn svg{width:18px;height:18px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
.cart-btn{
  position:relative;border:none;border-radius:100px;padding:10px 20px;font-size:13.5px;font-weight:600;
  display:flex;align-items:center;gap:8px;background:var(--grad);color:#fff;
  transition:transform .2s,box-shadow .2s;box-shadow:0 8px 18px -8px rgba(255,61,154,.5);
}
.cart-btn:hover{transform:translateY(-2px)}
.cart-btn:active{transform:scale(.96)}
.cart-count{
  min-width:20px;height:20px;border-radius:10px;background:#fff;color:var(--g1);
  font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;padding:0 5px;
  transition:transform .2s,opacity .2s;
}
.cart-count.zero{opacity:0;width:0;min-width:0;padding:0;margin-inline-start:-8px}
.cart-count.pop{transform:scale(1.4)}
.menu-btn{display:none;background:none;border:none;width:40px;height:40px}
.menu-btn span{display:block;width:22px;height:2px;background:var(--ink);margin:5px auto;transition:transform .25s,opacity .25s}

/* fly-to-cart dot */
.fly-dot{
  position:fixed;z-index:100;width:14px;height:14px;border-radius:50%;background:var(--grad);
  pointer-events:none;box-shadow:0 4px 10px rgba(255,61,154,.5);
}

/* ============ HERO ============ */
.hero{min-height:100svh;display:flex;align-items:center;position:relative;overflow:hidden;padding-top:calc(var(--nav-h) + var(--bar-h))}
.hero-glow{
  position:absolute;inset:auto -10% -30% -10%;height:70%;z-index:0;pointer-events:none;
  background:radial-gradient(60% 80% at 30% 100%,rgba(255,61,154,.16),transparent 70%),
             radial-gradient(50% 70% at 70% 100%,rgba(255,216,77,.2),transparent 70%);
}
.strand{position:absolute;inset:0;z-index:1;pointer-events:none}
.strand svg{width:100%;height:100%;display:block}
.hero-inner{position:relative;z-index:2;width:100%}
.hero h1{font-size:clamp(36px,5vw,68px);font-weight:800;max-width:15ch}
.hero h1 .shine{
  background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent;
  background-size:200% 100%;animation:sheen 6s ease-in-out infinite;
}
@keyframes sheen{0%,100%{background-position:0% 0}50%{background-position:100% 0}}
.hero-sub{margin-top:24px;max-width:48ch;color:var(--muted);font-size:clamp(15px,1.1vw,17px)}
.hero-cta-row{margin-top:38px;display:flex;gap:14px;flex-wrap:wrap}
/* staggered entrance */
.stagger{opacity:0;transform:translateY(24px);animation:rise .8s cubic-bezier(.2,.7,.2,1) forwards}
.stagger:nth-child(1){animation-delay:.05s}
.stagger:nth-child(2){animation-delay:.15s}
.stagger:nth-child(3){animation-delay:.28s}
.stagger:nth-child(4){animation-delay:.4s}
.stagger:nth-child(5){animation-delay:.52s}
@keyframes rise{to{opacity:1;transform:none}}
.btn{
  display:inline-flex;align-items:center;gap:10px;text-decoration:none;border-radius:100px;
  padding:15px 30px;font-size:15px;font-weight:600;border:1.5px solid transparent;
  transition:transform .2s,box-shadow .2s,background .2s,color .2s;
}
.btn:active{transform:scale(.97)}
.btn-solid{background:var(--grad);color:#fff;box-shadow:0 12px 26px -12px rgba(255,61,154,.55)}
.btn-solid:hover{transform:translateY(-2px)}
.btn-ghost{background:transparent;color:var(--ink);border-color:var(--line)}
.btn-ghost:hover{border-color:var(--g1);transform:translateY(-2px)}
.hero-meta{margin-top:60px;display:flex;flex-wrap:wrap;border-top:1px solid var(--line);max-width:640px}
.hero-meta div{padding:20px 28px 0 0;margin-inline-end:28px;border-inline-end:1px solid var(--line)}
[dir="rtl"] .hero-meta div{padding:20px 0 0 28px}
.hero-meta div:last-child{border-inline-end:none;margin-inline-end:0}
.hero-meta strong{font-family:var(--font-display);font-size:20px;display:block;font-weight:700}
[lang="ar"] .hero-meta strong{font-family:'Changa',sans-serif}
.hero-meta span{font-size:12.5px;color:var(--muted)}
.scroll-hint{
  position:absolute;bottom:26px;left:50%;transform:translateX(-50%);z-index:2;
  width:26px;height:42px;border:1.5px solid var(--muted);border-radius:16px;opacity:.6;
}
.scroll-hint::after{
  content:"";position:absolute;top:8px;left:50%;transform:translateX(-50%);
  width:4px;height:8px;border-radius:4px;background:var(--grad);
  animation:hint 1.8s ease-in-out infinite;
}
@keyframes hint{0%,100%{transform:translate(-50%,0);opacity:1}60%{transform:translate(-50%,14px);opacity:0}}

/* ============ SECTIONS ============ */
section{padding:110px 0}
.section-head{display:flex;justify-content:space-between;align-items:flex-end;gap:24px;margin-bottom:52px;flex-wrap:wrap}
.section-head h2{font-size:clamp(25px,3.2vw,38px);font-weight:700;margin-top:14px}
.section-head p{max-width:44ch;color:var(--muted);font-size:15px}
.reveal{opacity:0;transform:translateY(26px);transition:opacity .7s ease,transform .7s ease}
.reveal.in{opacity:1;transform:none}

/* ============ PRODUCTS ============ */
#products{padding-top:30px}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px}
.card{
  background:var(--surface);border:1px solid var(--line);border-radius:var(--radius);
  overflow:hidden;display:flex;flex-direction:column;transition:transform .3s,box-shadow .3s,border-color .3s;
}
.card:hover{transform:translateY(-6px);box-shadow:var(--shadow);border-color:var(--g2)}
.card-stage{
  height:260px;display:flex;align-items:flex-end;justify-content:center;
  background:var(--grad-soft);position:relative;overflow:hidden;cursor:pointer;border:none;width:100%;
}
.card-stage .num{
  position:absolute;top:16px;inset-inline-start:20px;font-family:var(--font-display);font-style:italic;
  font-weight:800;font-size:15px;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent;
}
.card-stage .view-tag{
  position:absolute;top:14px;inset-inline-end:16px;font-size:11.5px;font-weight:600;color:var(--ink);
  background:var(--surface);border:1px solid var(--line);border-radius:100px;padding:5px 12px;
  opacity:0;transform:translateY(-4px);transition:opacity .25s,transform .25s;
}
.card:hover .view-tag{opacity:1;transform:none}
.card-stage .shelf{position:absolute;bottom:44px;left:12%;right:12%;height:1.5px;background:rgba(66,32,47,.12)}
[data-theme="dark"] .card-stage .shelf{background:rgba(255,239,242,.14)}
.bottle{position:relative;z-index:2;margin-bottom:44px;transition:transform .35s}
.card:hover .bottle{transform:translateY(-7px) rotate(-1.5deg)}
.card-body{padding:22px 22px 24px;display:flex;flex-direction:column;gap:8px;flex:1}
.card-benefit{
  align-self:flex-start;font-size:12px;font-weight:600;padding:5px 12px;border-radius:100px;
  background:var(--grad-soft);border:1px solid var(--line);color:var(--ink);
}
.card-name{font-family:var(--font-display);font-weight:700;font-size:19px}
.card-desc{font-size:14px;color:var(--muted);flex:1}
.card-foot{display:flex;align-items:center;justify-content:space-between;margin-top:12px;gap:10px}
.price{font-weight:600;font-size:16px}
.add-btn{
  border:1.5px solid var(--ink);background:transparent;border-radius:100px;
  padding:9px 18px;font-size:13px;font-weight:600;transition:all .2s;white-space:nowrap;
}
.add-btn:hover,.add-btn.added{background:var(--ink);color:var(--bg)}
.add-btn:active{transform:scale(.95)}

/* CSS bottles */
.b-shape{border:1.5px solid var(--ink);background:var(--surface);position:relative}
.b-gloss{position:absolute;top:9%;inset-inline-start:14%;width:8px;height:58%;border-radius:8px;background:var(--grad);opacity:.8}
.b-tag{
  position:absolute;left:50%;top:52%;transform:translateX(-50%);width:72%;
  border-top:1px solid var(--line);border-bottom:1px solid var(--line);text-align:center;padding:4px 0;
}
.b-tag i{font-style:italic;font-family:var(--font-display);font-weight:800;font-size:8.5px;letter-spacing:.08em;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent}
.b-dropper{width:52px;height:120px;border-radius:10px 10px 14px 14px}
.b-dropper::before{content:"";position:absolute;top:-28px;left:50%;transform:translateX(-50%);width:17px;height:28px;background:var(--ink);border-radius:6px 6px 2px 2px}
.b-spray{width:58px;height:132px;border-radius:12px}
.b-spray::before{content:"";position:absolute;top:-24px;left:50%;transform:translateX(-50%);width:22px;height:24px;background:var(--ink);border-radius:6px;clip-path:polygon(0 0,100% 22%,100% 100%,0 100%)}
.b-tube{width:56px;height:126px;border-radius:8px 8px 18px 18px}
.b-tube::before{content:"";position:absolute;top:-13px;left:50%;transform:translateX(-50%);width:32px;height:13px;background:var(--ink);border-radius:5px 5px 0 0}

/* ============ RITUAL ============ */
.ritual{border-top:1px solid var(--line);border-bottom:1px solid var(--line);background:var(--surface)}
.ritual-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:22px}
.step{padding:28px;border:1px solid var(--line);border-radius:var(--radius);background:var(--bg);transition:transform .3s,box-shadow .3s}
.step:hover{transform:translateY(-4px);box-shadow:var(--shadow)}
.step b{
  display:inline-flex;width:34px;height:34px;border-radius:50%;background:var(--grad);color:#fff;
  align-items:center;justify-content:center;font-size:14px;margin-bottom:16px;font-family:var(--font-display);
}
.step h3{font-size:17px;margin-bottom:8px}
.step p{font-size:14px;color:var(--muted)}

/* ============ ABOUT ============ */
.about-grid{display:grid;grid-template-columns:1.05fr .95fr;gap:70px;align-items:center}
.about-copy p{color:var(--muted);margin-top:18px;max-width:54ch;font-size:15px}
.about-copy p strong{color:var(--ink);font-weight:600}
.pill-row{display:flex;gap:10px;flex-wrap:wrap;margin-top:28px}
.pill{border:1px solid var(--line);border-radius:100px;padding:8px 16px;font-size:13px;font-weight:500;color:var(--muted);background:var(--surface)}
.about-visual{position:relative;aspect-ratio:1/1.1;border-radius:var(--radius);border:1px solid var(--line);overflow:hidden;display:flex;align-items:center;justify-content:center;background:var(--surface)}
.about-visual .paint{position:absolute;inset:0;background:
  radial-gradient(45% 60% at 20% 30%,rgba(255,61,154,.22),transparent 70%),
  radial-gradient(45% 60% at 80% 25%,rgba(255,216,77,.3),transparent 70%),
  radial-gradient(55% 60% at 55% 85%,rgba(255,126,107,.25),transparent 70%)}
.about-visual .mark{
  position:relative;z-index:2;font-family:var(--font-display);font-style:italic;font-weight:800;
  font-size:clamp(34px,4.6vw,54px);text-transform:uppercase;
  background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent;
  animation:float 6s ease-in-out infinite;
}
[lang="ar"] .about-visual .mark{font-family:'Changa',sans-serif;animation-name:floatAr}
@keyframes float{0%,100%{transform:skewX(-4deg) translateY(-8px)}50%{transform:skewX(-4deg) translateY(8px)}}
@keyframes floatAr{0%,100%{transform:translateY(-8px)}50%{transform:translateY(8px)}}

/* ============ REVIEWS ============ */
.reviews-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:22px}
.review{
  background:var(--surface);border:1px solid var(--line);border-radius:var(--radius);
  padding:28px;display:flex;flex-direction:column;gap:14px;transition:transform .3s,box-shadow .3s;
}
.review:hover{transform:translateY(-4px);box-shadow:var(--shadow)}
.stars{display:flex;gap:3px}
.stars svg{width:16px;height:16px;fill:url(#starGrad)}
.review p{font-size:14.5px;flex:1}
.review-who{display:flex;align-items:center;gap:12px}
.avatar{
  width:40px;height:40px;border-radius:50%;background:var(--grad);color:#fff;
  display:flex;align-items:center;justify-content:center;font-weight:700;font-size:14px;flex-shrink:0;
}
.review-who b{font-size:14px;display:block}
.review-who span{font-size:12.5px;color:var(--muted)}

/* ============ FAQ ============ */
.faq{border-top:1px solid var(--line);background:var(--surface)}
.faq-list{max-width:760px}
.faq-item{border-bottom:1px solid var(--line)}
.faq-item:first-child{border-top:1px solid var(--line)}
.faq-q{
  width:100%;background:none;border:none;text-align:start;
  display:flex;justify-content:space-between;align-items:center;gap:16px;
  padding:22px 4px;font-size:16.5px;font-weight:600;transition:color .2s;
}
.faq-q:hover{color:var(--g1)}
.faq-q .chev{
  width:30px;height:30px;border-radius:50%;border:1.5px solid var(--line);flex-shrink:0;
  display:flex;align-items:center;justify-content:center;transition:transform .3s,background .3s,border-color .3s;
}
.faq-q .chev svg{width:13px;height:13px;stroke:currentColor;fill:none;stroke-width:2;stroke-linecap:round}
.faq-item.open .chev{transform:rotate(180deg);background:var(--grad);border-color:transparent;color:#fff}
.faq-a{max-height:0;overflow:hidden;transition:max-height .35s ease}
.faq-a p{padding:0 4px 22px;color:var(--muted);font-size:15px;max-width:60ch}

/* ============ FOOTER ============ */
footer{border-top:1px solid var(--line);padding:64px 0 40px;background:var(--bg)}
.foot-grid{display:flex;justify-content:space-between;gap:48px;flex-wrap:wrap;align-items:flex-start}
.foot-note{font-size:13px;color:var(--muted);max-width:34ch;margin-top:12px}
.foot-links{display:flex;gap:48px;flex-wrap:wrap}
.foot-links ul{list-style:none;display:flex;flex-direction:column;gap:10px}
.foot-links b{font-size:12px;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);display:block;margin-bottom:14px;font-weight:600}
[lang="ar"] .foot-links b{letter-spacing:.04em}
.foot-links a{text-decoration:none;font-size:14px;opacity:.85}
.foot-links a:hover{opacity:1}
.newsletter{max-width:320px}
.newsletter p{font-size:13.5px;color:var(--muted);margin:12px 0 16px}
.newsletter-row{display:flex;gap:8px}
.newsletter-row input{
  flex:1;min-width:0;border:1.5px solid var(--line);border-radius:100px;background:var(--surface);
  padding:11px 18px;font-family:inherit;font-size:14px;color:var(--ink);transition:border-color .2s;
}
.newsletter-row input:focus{outline:none;border-color:var(--g1)}
.newsletter-row button{
  border:none;border-radius:100px;background:var(--grad);color:#fff;padding:11px 20px;
  font-size:13.5px;font-weight:600;white-space:nowrap;transition:transform .2s;
}
.newsletter-row button:hover{transform:translateY(-1px)}
.foot-base{margin-top:48px;padding-top:24px;border-top:1px solid var(--line);display:flex;justify-content:space-between;gap:16px;flex-wrap:wrap;font-size:12.5px;color:var(--muted)}

/* ============ DRAWERS / MODALS ============ */
.overlay{position:fixed;inset:0;background:rgba(40,12,26,.42);z-index:70;opacity:0;pointer-events:none;transition:opacity .3s;backdrop-filter:blur(2px)}
.overlay.open{opacity:1;pointer-events:auto}
.drawer{
  position:fixed;top:0;inset-inline-end:0;bottom:0;width:min(420px,100%);z-index:80;
  background:var(--surface);border-inline-start:1px solid var(--line);
  transform:translateX(100%);transition:transform .35s cubic-bezier(.32,.72,.25,1);
  display:flex;flex-direction:column;
}
[dir="rtl"] .drawer{transform:translateX(-100%)}
.drawer.open{transform:none!important}
.drawer-head{padding:22px 26px;border-bottom:1px solid var(--line);display:flex;justify-content:space-between;align-items:center}
.drawer-head h3{font-size:20px;font-weight:700}
.close-btn{background:none;border:none;font-size:26px;line-height:1;padding:4px 10px;color:var(--muted);border-radius:8px}
.close-btn:hover{color:var(--ink)}
/* free shipping bar */
.ship-bar{padding:16px 26px 0}
.ship-bar p{font-size:12.5px;color:var(--muted);margin-bottom:8px}
.ship-bar p b{color:var(--ink)}
.ship-track{height:6px;border-radius:6px;background:var(--line);overflow:hidden}
.ship-fill{height:100%;width:0;background:var(--grad);border-radius:6px;transition:width .5s cubic-bezier(.2,.7,.2,1)}
.drawer-items{flex:1;overflow-y:auto;padding:10px 26px}
.cart-empty{padding:48px 0;text-align:center;color:var(--muted);font-size:14.5px;display:flex;flex-direction:column;gap:18px;align-items:center}
.cart-item{display:flex;gap:16px;align-items:center;padding:18px 0;border-bottom:1px solid var(--line);animation:itemIn .3s ease}
@keyframes itemIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.cart-thumb{
  width:54px;height:54px;border-radius:14px;background:var(--grad-soft);border:1px solid var(--line);
  flex-shrink:0;display:flex;align-items:center;justify-content:center;
  font-family:var(--font-display);font-style:italic;font-weight:800;font-size:11px;
}
.cart-thumb i{font-style:italic;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent}
.cart-item-info{flex:1;min-width:0}
.cart-item-info b{font-size:14.5px;display:block}
.cart-item-info span{font-size:13px;color:var(--muted)}
.qty{display:flex;align-items:center;gap:2px;border:1.5px solid var(--line);border-radius:100px}
.qty button{background:none;border:none;width:28px;height:28px;font-size:15px;color:var(--muted);border-radius:50%}
.qty button:hover{color:var(--ink)}
.qty span{font-size:13px;font-weight:600;min-width:18px;text-align:center}
.remove-btn{background:none;border:none;font-size:12px;color:var(--muted);text-decoration:underline;padding:2px}
.remove-btn:hover{color:var(--ink)}
.drawer-foot{padding:22px 26px;border-top:1px solid var(--line)}
.subtotal{display:flex;justify-content:space-between;font-weight:600;font-size:16px;margin-bottom:6px}
.drawer-foot .form-note{font-size:12.5px;color:var(--muted);margin-bottom:14px}
.checkout-btn{
  width:100%;border:none;background:var(--grad);color:#fff;border-radius:100px;
  padding:16px;font-size:15px;font-weight:600;transition:opacity .2s,transform .2s;
}
.checkout-btn:hover{opacity:.92;transform:translateY(-1px)}
.checkout-btn:active{transform:scale(.98)}

/* product modal */
.modal{
  position:fixed;inset:0;z-index:82;display:flex;align-items:center;justify-content:center;padding:20px;
  opacity:0;pointer-events:none;transition:opacity .3s;
}
.modal.open{opacity:1;pointer-events:auto}
.modal-card{
  width:min(880px,100%);max-height:min(640px,92svh);overflow:auto;background:var(--surface);
  border:1px solid var(--line);border-radius:24px;display:grid;grid-template-columns:1fr 1.15fr;
  transform:translateY(16px) scale(.98);transition:transform .3s cubic-bezier(.2,.7,.2,1);position:relative;
}
.modal.open .modal-card{transform:none}
.modal-stage{background:var(--grad-soft);display:flex;align-items:flex-end;justify-content:center;position:relative;min-height:320px}
.modal-stage .shelf{position:absolute;bottom:56px;left:14%;right:14%;height:1.5px;background:rgba(66,32,47,.12)}
[data-theme="dark"] .modal-stage .shelf{background:rgba(255,239,242,.14)}
.modal-stage .bottle{margin-bottom:56px;transform:scale(1.3);transform-origin:bottom}
.modal-info{padding:34px 34px 30px;display:flex;flex-direction:column;gap:14px}
.modal-close{
  position:absolute;top:14px;inset-inline-end:14px;z-index:2;width:38px;height:38px;border-radius:50%;
  border:1px solid var(--line);background:var(--surface);font-size:20px;color:var(--muted);
}
.modal-close:hover{color:var(--ink)}
.modal-info .card-benefit{margin-top:4px}
.modal-info h3{font-size:26px}
.modal-info .m-desc{font-size:14.5px;color:var(--muted)}
.m-features{list-style:none;display:flex;flex-direction:column;gap:9px;margin:4px 0}
.m-features li{display:flex;gap:10px;align-items:flex-start;font-size:14px}
.m-features li::before{
  content:"";width:16px;height:16px;flex-shrink:0;margin-top:3px;border-radius:50%;
  background:var(--grad);
  -webkit-mask:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='black' stroke-width='3.4' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M20 6L9 17l-5-5'/%3E%3C/svg%3E") center/contain no-repeat;
  mask:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='black' stroke-width='3.4' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M20 6L9 17l-5-5'/%3E%3C/svg%3E") center/contain no-repeat;
}
.m-howto{font-size:13.5px;color:var(--muted);background:var(--bg);border:1px solid var(--line);border-radius:14px;padding:14px 16px}
.m-howto b{color:var(--ink);display:block;margin-bottom:4px;font-size:13px}
.modal-foot{margin-top:auto;display:flex;align-items:center;gap:14px;flex-wrap:wrap;padding-top:8px}
.modal-foot .price{font-size:22px;font-family:var(--font-display);font-weight:700}
[lang="ar"] .modal-foot .price{font-family:'Changa',sans-serif}
.modal-foot .qty{border-color:var(--line)}
.modal-foot .qty button{width:34px;height:34px}
.modal-add{
  flex:1;min-width:150px;border:none;border-radius:100px;background:var(--grad);color:#fff;
  padding:14px 22px;font-size:14.5px;font-weight:600;transition:transform .2s,opacity .2s;
}
.modal-add:hover{opacity:.92;transform:translateY(-1px)}
.modal-add:active{transform:scale(.97)}

/* settings panel */
.settings-panel{
  position:fixed;top:calc(var(--nav-h) + var(--announce-offset) + 10px);inset-inline-end:24px;z-index:85;width:280px;
  background:var(--surface);border:1px solid var(--line);border-radius:18px;box-shadow:var(--shadow);
  padding:20px;opacity:0;transform:translateY(-8px);pointer-events:none;transition:opacity .25s,transform .25s;
}
.settings-panel.open{opacity:1;transform:none;pointer-events:auto}
.settings-panel h4{font-size:15px;font-weight:700;margin-bottom:16px;font-family:var(--font-display)}
.setting{margin-bottom:16px}
.setting:last-child{margin-bottom:0}
.setting label{display:block;font-size:12px;font-weight:600;color:var(--muted);margin-bottom:8px;letter-spacing:.06em;text-transform:uppercase}
[lang="ar"] .setting label{letter-spacing:0}
.seg{display:flex;border:1.5px solid var(--line);border-radius:100px;overflow:hidden}
.seg button{flex:1;border:none;background:transparent;padding:9px 6px;font-size:13px;font-weight:600;color:var(--muted);transition:background .2s,color .2s}
.seg button.active{background:var(--grad);color:#fff}

/* back to top */
.to-top{
  position:fixed;bottom:24px;inset-inline-end:24px;z-index:55;width:46px;height:46px;border-radius:50%;
  border:none;background:var(--grad);color:#fff;box-shadow:0 10px 22px -10px rgba(255,61,154,.6);
  display:flex;align-items:center;justify-content:center;
  opacity:0;transform:translateY(12px);pointer-events:none;transition:opacity .3s,transform .3s;
}
.to-top.show{opacity:1;transform:none;pointer-events:auto}
.to-top:hover{transform:translateY(-2px)}
.to-top svg{width:18px;height:18px;stroke:#fff;fill:none;stroke-width:2.2;stroke-linecap:round;stroke-linejoin:round}

/* toast */
.toast{
  position:fixed;bottom:28px;left:50%;transform:translate(-50%,80px);z-index:95;
  background:var(--ink);color:var(--bg);border-radius:100px;padding:13px 26px;
  font-size:14px;font-weight:500;opacity:0;transition:transform .35s,opacity .35s;
  pointer-events:none;max-width:calc(100vw - 40px);text-align:center;
}
.toast.show{transform:translate(-50%,0);opacity:1}

/* ============ RESPONSIVE ============ */
@media(max-width:960px){
  .grid,.ritual-grid,.reviews-grid{grid-template-columns:1fr 1fr}
  .about-grid{grid-template-columns:1fr;gap:48px}
  .about-visual{max-width:420px}
  .modal-card{grid-template-columns:1fr;max-height:92svh}
  .modal-stage{min-height:240px}
  .modal-stage .bottle{transform:scale(1.1);transform-origin:bottom}
}
@media(max-width:720px){
  section{padding:80px 0}
  .announce{font-size:12px;padding:0 40px}
  .nav-links{
    position:fixed;top:calc(var(--nav-h) + var(--announce-offset));left:0;right:0;background:var(--bg);
    flex-direction:column;gap:0;padding:12px 24px 24px;border-bottom:1px solid var(--line);
    transform:translateY(-12px);opacity:0;pointer-events:none;transition:.25s;
  }
  .nav-links.open{transform:none;opacity:1;pointer-events:auto}
  .nav-links a{display:block;padding:14px 0;font-size:16px;border-bottom:1px solid var(--line);border-radius:0}
  .nav-links a.active{background:none;color:var(--g1)}
  .menu-btn{display:block}
  .menu-btn.open span:nth-child(1){transform:translateY(7px) rotate(45deg)}
  .menu-btn.open span:nth-child(2){opacity:0}
  .menu-btn.open span:nth-child(3){transform:translateY(-7px) rotate(-45deg)}
  .grid,.ritual-grid,.reviews-grid{grid-template-columns:1fr}
  .hero-meta div{border-inline-end:none;padding-inline-end:0;margin-inline-end:20px}
  .cart-btn .cart-label{display:none}
  .settings-panel{inset-inline-end:12px;inset-inline-start:12px;width:auto}
  .scroll-hint{display:none}
  .to-top{bottom:18px;inset-inline-end:16px}
}
@media(max-width:460px){
  body{font-size:15px}
  .wrap{padding:0 18px}
  .nav-inner{padding:0 16px}
  section{padding:64px 0}
  .hero h1{font-size:clamp(32px,9vw,40px)}
  .hero-sub{font-size:14.5px}
  .hero-cta-row{width:100%}
  .hero-cta-row .btn{flex:1;justify-content:center;padding:14px 18px;font-size:14px}
  .hero-meta{margin-top:44px}
  .hero-meta div{padding-top:16px}
  .section-head{margin-bottom:36px}
  .card-stage{height:230px}
  .modal-info{padding:26px 22px 24px}
  .modal-info h3{font-size:21px}
  .modal-foot .price{font-size:19px}
  .drawer-head,.drawer-items,.drawer-foot{padding-left:20px;padding-right:20px}
  .ship-bar{padding-left:20px;padding-right:20px}
  .announce{font-size:11.5px}
  .icon-btn{width:38px;height:38px}
  .cart-btn{padding:9px 14px}
}
@media(min-width:1600px){
  body{font-size:17px}
  .wrap,.nav-inner{max-width:1140px}
}
</style>
</head>
<body class="announce-on">

<!-- SVG defs for gradient stars -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <linearGradient id="starGrad" x1="0" y1="0" x2="1" y2="0">
      <stop offset="0" stop-color="#FF3D9A"/><stop offset=".5" stop-color="#FF9A62"/><stop offset="1" stop-color="#FFD84D"/>
    </linearGradient>
  </defs>
</svg>

<!-- ============ ANNOUNCEMENT ============ -->
<div class="announce" id="announce">
  <span data-i18n="announce">Free shipping on orders over SAR 150 ✨</span>
  <button id="announceClose" aria-label="Dismiss">×</button>
</div>

<!-- ============ NAV ============ -->
<header class="nav" id="nav">
  <div class="nav-inner">
    <a class="wordmark" href="#home" aria-label="Luméra — home">Luméra</a>
    <nav aria-label="Main">
      <ul class="nav-links" id="navLinks">
        <li><a href="#home" data-spy="home" data-i18n="nav_home">Home</a></li>
        <li><a href="#products" data-spy="products" data-i18n="nav_products">Products</a></li>
        <li><a href="#about" data-spy="about" data-i18n="nav_about">About</a></li>
        <li><a href="#faq" data-spy="faq" data-i18n="nav_faq">FAQ</a></li>
      </ul>
    </nav>
    <div class="nav-actions">
      <button class="icon-btn" id="settingsBtn" aria-label="Settings" aria-expanded="false">
        <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.7 1.7 0 0 0 .34 1.87l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.7 1.7 0 0 0-1.87-.34 1.7 1.7 0 0 0-1 1.55V21a2 2 0 1 1-4 0v-.09a1.7 1.7 0 0 0-1-1.55 1.7 1.7 0 0 0-1.87.34l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06a1.7 1.7 0 0 0 .34-1.87 1.7 1.7 0 0 0-1.55-1H3a2 2 0 1 1 0-4h.09a1.7 1.7 0 0 0 1.55-1 1.7 1.7 0 0 0-.34-1.87l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06a1.7 1.7 0 0 0 1.87.34h.01a1.7 1.7 0 0 0 1-1.55V3a2 2 0 1 1 4 0v.09a1.7 1.7 0 0 0 1 1.55 1.7 1.7 0 0 0 1.87-.34l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06a1.7 1.7 0 0 0-.34 1.87v.01a1.7 1.7 0 0 0 1.55 1H21a2 2 0 1 1 0 4h-.09a1.7 1.7 0 0 0-1.55 1z"/></svg>
      </button>
      <button class="cart-btn" id="cartOpen" aria-label="Open cart">
        <span class="cart-label" data-i18n="cart">Cart</span> <span class="cart-count zero" id="cartCount">0</span>
      </button>
      <button class="menu-btn" id="menuBtn" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
    </div>
  </div>
</header>
<div class="progress" id="progress"></div>

<!-- settings panel -->
<div class="settings-panel" id="settingsPanel" aria-label="Settings">
  <h4 data-i18n="settings_title">Settings</h4>
  <div class="setting">
    <label data-i18n="settings_lang">Language</label>
    <div class="seg" role="group" aria-label="Language">
      <button id="langEn" class="active">English</button>
      <button id="langAr">العربية</button>
    </div>
  </div>
  <div class="setting">
    <label data-i18n="settings_theme">Theme</label>
    <div class="seg" role="group" aria-label="Theme">
      <button id="themeLight" class="active" data-i18n="theme_light">Light</button>
      <button id="themeDark" data-i18n="theme_dark">Dark</button>
    </div>
  </div>
</div>

<main>
<!-- ============ HERO ============ -->
<section class="hero" id="home">
  <div class="hero-glow" aria-hidden="true"></div>
  <div class="strand" aria-hidden="true">
    <svg viewBox="0 0 1440 900" preserveAspectRatio="xMidYMid slice" fill="none">
      <defs>
        <linearGradient id="lumGrad" x1="0" y1="0" x2="1440" y2="0" gradientUnits="userSpaceOnUse">
          <stop offset="0" stop-color="#FF3D9A"/><stop offset=".38" stop-color="#FF7E6B"/>
          <stop offset=".68" stop-color="#FFB25C"/><stop offset="1" stop-color="#FFD84D"/>
        </linearGradient>
      </defs>
      <path d="M-60 640 C 260 560, 420 780, 740 660 S 1240 420, 1520 560" stroke="url(#lumGrad)" stroke-width="90" stroke-linecap="round" opacity=".28"/>
      <path d="M-60 660 C 260 580, 420 800, 740 680 S 1240 440, 1520 580" stroke="url(#lumGrad)" stroke-width="32" stroke-linecap="round" opacity=".65"/>
    </svg>
  </div>
  <div class="wrap hero-inner">
    <p class="eyebrow stagger" data-i18n="hero_eyebrow">Radiant hair care</p>
    <h1 style="margin-top:22px" id="heroTitle" class="stagger"></h1>
    <p class="hero-sub stagger" data-i18n="hero_sub">Three essentials — an oil, a detangler and a cream — made to grow, soften and light up every hair type.</p>
    <div class="hero-cta-row stagger">
      <a class="btn btn-solid" href="#products" data-i18n="hero_cta1">Shop the range</a>
      <a class="btn btn-ghost" href="#about" data-i18n="hero_cta2">Our story</a>
    </div>
    <div class="hero-meta stagger">
      <div><strong>3</strong><span data-i18n="meta1">daily essentials</span></div>
      <div><strong>0</strong><span data-i18n="meta2">sulfates &amp; parabens</span></div>
      <div><strong>100%</strong><span data-i18n="meta3">made with love</span></div>
    </div>
  </div>
  <div class="scroll-hint" aria-hidden="true"></div>
</section>

<!-- ============ PRODUCTS ============ -->
<section id="products">
  <div class="wrap">
    <div class="section-head reveal">
      <div>
        <p class="eyebrow" data-i18n="products_eyebrow">The range</p>
        <h2 data-i18n="products_title">Three steps to<br>luminous hair.</h2>
      </div>
      <p data-i18n="products_sub">A complete routine in three products. Tap any product to see the full details.</p>
    </div>
    <div class="grid" id="productGrid"></div>
  </div>
</section>

<!-- ============ RITUAL ============ -->
<section class="ritual">
  <div class="wrap">
    <div class="section-head reveal">
      <div>
        <p class="eyebrow" data-i18n="ritual_eyebrow">The ritual</p>
        <h2 data-i18n="ritual_title">How to use them together</h2>
      </div>
    </div>
    <div class="ritual-grid">
      <div class="step reveal"><b>1</b><h3 data-i18n="step1_t">Detangle</h3><p data-i18n="step1_p">Mist the detangler through damp or dry hair and brush through gently — no pulling, no breakage.</p></div>
      <div class="step reveal"><b>2</b><h3 data-i18n="step2_t">Hydrate</h3><p data-i18n="step2_p">Work a small amount of hair cream from mid-lengths to ends to lock in softness and moisture.</p></div>
      <div class="step reveal"><b>3</b><h3 data-i18n="step3_t">Shine &amp; grow</h3><p data-i18n="step3_p">Finish with a few drops of hair oil on the ends and scalp to boost length, thickness and gloss.</p></div>
    </div>
  </div>
</section>

<!-- ============ ABOUT ============ -->
<section id="about">
  <div class="wrap">
    <div class="about-grid">
      <div class="about-copy reveal">
        <p class="eyebrow" data-i18n="about_eyebrow">About Luméra</p>
        <h2 style="font-size:clamp(24px,3vw,34px);margin-top:14px" data-i18n="about_title">Named after light.<br>Made for shine.</h2>
        <p data-i18n="about_p1">Luméra comes from "lumière" — light. We believe healthy hair doesn't need a shelf full of products; it needs a few honest ones that actually work.</p>
        <p data-i18n="about_p2">So we made exactly three: an oil that helps hair grow longer and thicker, a spray that melts away tangles, and a cream that keeps every strand deeply hydrated. Nothing more, nothing less.</p>
        <div class="pill-row">
          <span class="pill" data-i18n="pill1">Vegan &amp; cruelty-free</span>
          <span class="pill" data-i18n="pill2">All hair types</span>
          <span class="pill" data-i18n="pill3">Gentle daily formulas</span>
        </div>
      </div>
      <div class="about-visual reveal" aria-hidden="true">
        <div class="paint"></div>
        <span class="mark">Luméra</span>
      </div>
    </div>
  </div>
</section>

<!-- ============ REVIEWS ============ -->
<section id="reviews" style="padding-top:0">
  <div class="wrap">
    <div class="section-head reveal">
      <div>
        <p class="eyebrow" data-i18n="reviews_eyebrow">Loved already</p>
        <h2 data-i18n="reviews_title">What early users say</h2>
      </div>
    </div>
    <div class="reviews-grid" id="reviewsGrid"></div>
  </div>
</section>

<!-- ============ FAQ ============ -->
<section class="faq" id="faq">
  <div class="wrap">
    <div class="section-head reveal">
      <div>
        <p class="eyebrow" data-i18n="faq_eyebrow">Questions</p>
        <h2 data-i18n="faq_title">Everything you're wondering</h2>
      </div>
    </div>
    <div class="faq-list" id="faqList"></div>
  </div>
</section>
</main>

<!-- ============ FOOTER ============ -->
<footer>
  <div class="wrap">
    <div class="foot-grid">
      <div>
        <a class="wordmark" href="#home">Luméra</a>
        <p class="foot-note" data-i18n="foot_note">Radiant hair care in three honest steps. Demo storefront.</p>
      </div>
      <div class="foot-links">
        <ul>
          <b data-i18n="foot_shop">Shop</b>
          <li><a href="#products" data-i18n="p1_name">Hair Oil</a></li>
          <li><a href="#products" data-i18n="p2_name">Detangler Spray</a></li>
          <li><a href="#products" data-i18n="p3_name">Hair Cream</a></li>
        </ul>
        <ul>
          <b data-i18n="foot_company">Company</b>
          <li><a href="#about" data-i18n="nav_about">About</a></li>
          <li><a href="#faq" data-i18n="nav_faq">FAQ</a></li>
          <li><a href="mailto:hello@lumera.example">hello@lumera.example</a></li>
        </ul>
      </div>
      <div class="newsletter">
        <b style="font-size:12px;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);font-weight:600" data-i18n="nl_title">Stay in the light</b>
        <p data-i18n="nl_sub">Launches, tips and early offers. No spam, ever.</p>
        <div class="newsletter-row">
          <input type="email" id="nlEmail" data-i18n-ph="nl_ph" placeholder="you@email.com" aria-label="Email">
          <button id="nlBtn" data-i18n="nl_btn">Subscribe</button>
        </div>
      </div>
    </div>
    <div class="foot-base">
      <span data-i18n="foot_c">© 2026 Luméra. Demo site.</span>
      <span data-i18n="foot_tag">Hair that catches the light.</span>
    </div>
  </div>
</footer>

<!-- back to top -->
<button class="to-top" id="toTop" aria-label="Back to top">
  <svg viewBox="0 0 24 24"><path d="M12 19V5M5 12l7-7 7 7"/></svg>
</button>

<!-- ============ CART ============ -->
<div class="overlay" id="overlay"></div>
<aside class="drawer" id="drawer" aria-label="Shopping cart" aria-hidden="true">
  <div class="drawer-head">
    <h3 data-i18n="cart_title">Your cart</h3>
    <button class="close-btn" id="cartClose" aria-label="Close cart">×</button>
  </div>
  <div class="ship-bar" id="shipBar">
    <p id="shipMsg"></p>
    <div class="ship-track"><div class="ship-fill" id="shipFill"></div></div>
  </div>
  <div class="drawer-items" id="cartItems"></div>
  <div class="drawer-foot">
    <div class="subtotal"><span data-i18n="cart_subtotal">Subtotal</span><span id="subtotal">0</span></div>
    <p class="form-note" data-i18n="cart_note">Demo cart — no real payments are processed.</p>
    <button class="checkout-btn" id="checkoutBtn" data-i18n="cart_checkout">Checkout</button>
  </div>
</aside>

<!-- ============ PRODUCT MODAL ============ -->
<div class="modal" id="modal" role="dialog" aria-modal="true" aria-hidden="true">
  <div class="modal-card" id="modalCard"></div>
</div>

<div class="toast" id="toast" role="status" aria-live="polite"></div>

<script>
/* ============ DATA ============ */
const FREE_SHIP = 150;
const PRODUCTS = [
  {id:1, price:79, shape:"b-dropper", size:"50ml",
   en:{name:"Luméra Hair Oil", benefit:"Lengthens & thickens",
       desc:"A nourishing daily oil that strengthens roots and coats each strand — for longer, thicker, glossier hair.",
       features:["Boosts length & thickness over time","Strengthens roots and reduces fall","Adds mirror-like shine without grease"],
       howto:"Massage 3–5 drops into the scalp and ends, day or night. Use daily for best results."},
   ar:{name:"زيت لوميرا للشعر", benefit:"يطوّل ويكثّف",
       desc:"زيت يومي مغذٍّ يقوّي الجذور ويغلّف كل خصلة — لشعر أطول وأكثف وأكثر لمعانًا.",
       features:["يعزّز الطول والكثافة مع الاستخدام","يقوّي الجذور ويقلّل التساقط","لمعان صافٍ دون ملمس دهني"],
       howto:"دلّكي فروة الرأس والأطراف بـ 3–5 قطرات صباحًا أو مساءً. استخدميه يوميًا لأفضل النتائج."}},
  {id:2, price:59, shape:"b-spray", size:"120ml",
   en:{name:"Detangler Spray", benefit:"Detangles instantly",
       desc:"A weightless leave-in mist that melts knots on contact, so brushing glides — no pulling, no breakage.",
       features:["Melts tangles in seconds","Zero pulling, zero breakage","Light enough for daily use"],
       howto:"Mist over damp or dry hair, wait a few seconds, then brush from the ends upward."},
   ar:{name:"بخاخ فك التشابك", benefit:"يفك التشابك فورًا",
       desc:"بخاخ خفيف يُترك على الشعر يذيب العقد فور ملامستها، فينساب المشط بسهولة — دون شدّ أو تقصّف.",
       features:["يفك العقد خلال ثوانٍ","دون شدّ أو تقصّف","خفيف يناسب الاستخدام اليومي"],
       howto:"رشّيه على الشعر الرطب أو الجاف، انتظري ثوانٍ، ثم مشّطي من الأطراف إلى الأعلى."}},
  {id:3, price:69, shape:"b-tube", size:"150ml",
   en:{name:"Hair Cream", benefit:"Deep hydration",
       desc:"A rich yet airy cream that seals in moisture from mid-lengths to ends, keeping hair soft all day.",
       features:["24-hour deep hydration","Softens and smooths frizz","Never heavy, never sticky"],
       howto:"Warm a coin-sized amount between palms and apply from mid-lengths to ends on damp hair."},
   ar:{name:"كريم الشعر", benefit:"للترطيب العميق",
       desc:"كريم غني وخفيف يحبس الترطيب من منتصف الشعر حتى الأطراف، ليبقى ناعمًا طوال اليوم.",
       features:["ترطيب عميق يدوم 24 ساعة","ينعّم الشعر ويهدّئ التجعّد","خفيف دون ثقل أو لزوجة"],
       howto:"دفّئي كمية بحجم عملة بين راحتيك ووزّعيها من منتصف الشعر حتى الأطراف على شعر رطب."}},
];
const REVIEWS = [
  {init:"S", en:{text:"My hair stopped snapping when I brush it. The detangler is genuinely magic — my mornings are five minutes shorter.", name:"Sara M.", tag:"Detangler Spray"},
              ar:{text:"شعري ما عاد يتقصّف عند التمشيط. البخاخ سحر فعلًا — صباحاتي صارت أقصر بخمس دقائق.", name:"سارة م.", tag:"بخاخ فك التشابك"}},
  {init:"N", en:{text:"Three months on the oil and my baby hairs are filling in. It smells soft and never feels greasy.", name:"Noura A.", tag:"Hair Oil"},
              ar:{text:"ثلاثة أشهر على الزيت وبدأ الشعر الجديد يظهر. رائحته ناعمة ولا يترك ملمسًا دهنيًا أبدًا.", name:"نورة أ.", tag:"زيت الشعر"}},
  {init:"L", en:{text:"The cream keeps my curls soft until the evening without weighing them down. I've repurchased twice already.", name:"Layla K.", tag:"Hair Cream"},
              ar:{text:"الكريم يحافظ على نعومة تموّجاتي حتى المساء دون أن يثقلها. أعدت شراءه مرتين حتى الآن.", name:"ليلى ك.", tag:"كريم الشعر"}},
];
const FAQS = [
  {en:{q:"Which product should I start with?", a:"If tangles are your struggle, start with the Detangler Spray. For dryness, the Hair Cream. For growth and thickness, the Hair Oil. Together they make one complete routine — detangle, hydrate, then shine."},
   ar:{q:"بأي منتج أبدأ؟", a:"إذا كان التشابك مشكلتك، ابدئي ببخاخ فك التشابك. للجفاف، كريم الشعر. للنمو والكثافة، زيت الشعر. ومعًا تشكّل روتينًا متكاملًا — فكّي التشابك، رطّبي، ثم أضيفي اللمعان."}},
  {en:{q:"Do the products suit all hair types?", a:"Yes — every formula is tested on straight, wavy, curly and coily hair, and they're gentle enough for color-treated hair too."},
   ar:{q:"هل تناسب المنتجات كل أنواع الشعر؟", a:"نعم — كل تركيبة مختبرة على الشعر الأملس والمموّج والمجعّد والكثيف، وهي لطيفة بما يكفي للشعر المصبوغ أيضًا."}},
  {en:{q:"How long until I see results?", a:"The detangler and cream work from the first use. The oil builds results over time — most people notice softer, fuller hair within 4–8 weeks of daily use."},
   ar:{q:"متى أرى النتائج؟", a:"البخاخ والكريم يعملان من أول استخدام. أما الزيت فنتائجه تراكمية — يلاحظ معظم المستخدمين شعرًا أنعم وأكثف خلال 4–8 أسابيع من الاستخدام اليومي."}},
  {en:{q:"Is shipping really free?", a:"On orders over SAR 150, yes — which happens to be any two products together. Orders below that ship at a flat rate."},
   ar:{q:"هل الشحن مجاني فعلًا؟", a:"نعم للطلبات فوق 150 ر.س — أي عند شراء منتجين معًا. الطلبات الأقل تُشحن برسوم ثابتة."}},
];

/* ============ TRANSLATIONS ============ */
const I18N = {
en:{
  announce:"Free shipping on orders over SAR 150 ✨",
  nav_home:"Home", nav_products:"Products", nav_about:"About", nav_faq:"FAQ", cart:"Cart",
  settings_title:"Settings", settings_lang:"Language", settings_theme:"Theme", theme_light:"Light", theme_dark:"Dark",
  hero_eyebrow:"Radiant hair care",
  hero_title:'Hair that<br>catches <span class="shine">the light</span>.',
  hero_sub:"Three essentials — an oil, a detangler and a cream — made to grow, soften and light up every hair type.",
  hero_cta1:"Shop the range", hero_cta2:"Our story",
  meta1:"daily essentials", meta2:"sulfates & parabens", meta3:"made with love",
  products_eyebrow:"The range", products_title:"Three steps to<br>luminous hair.",
  products_sub:"A complete routine in three products. Tap any product to see the full details.",
  view_details:"View details",
  ritual_eyebrow:"The ritual", ritual_title:"How to use them together",
  step1_t:"Detangle", step1_p:"Mist the detangler through damp or dry hair and brush through gently — no pulling, no breakage.",
  step2_t:"Hydrate", step2_p:"Work a small amount of hair cream from mid-lengths to ends to lock in softness and moisture.",
  step3_t:"Shine & grow", step3_p:"Finish with a few drops of hair oil on the ends and scalp to boost length, thickness and gloss.",
  about_eyebrow:"About Luméra", about_title:"Named after light.<br>Made for shine.",
  about_p1:'Luméra comes from "lumière" — light. We believe healthy hair doesn\'t need a shelf full of products; it needs a few honest ones that actually work.',
  about_p2:"So we made exactly three: an oil that helps hair grow longer and thicker, a spray that melts away tangles, and a cream that keeps every strand deeply hydrated. Nothing more, nothing less.",
  pill1:"Vegan & cruelty-free", pill2:"All hair types", pill3:"Gentle daily formulas",
  reviews_eyebrow:"Loved already", reviews_title:"What early users say",
  faq_eyebrow:"Questions", faq_title:"Everything you're wondering",
  foot_note:"Radiant hair care in three honest steps. Demo storefront.",
  foot_shop:"Shop", foot_company:"Company",
  p1_name:"Hair Oil", p2_name:"Detangler Spray", p3_name:"Hair Cream",
  nl_title:"Stay in the light", nl_sub:"Launches, tips and early offers. No spam, ever.",
  nl_ph:"you@email.com", nl_btn:"Subscribe",
  foot_c:"© 2026 Luméra. Demo site.", foot_tag:"Hair that catches the light.",
  cart_title:"Your cart", cart_subtotal:"Subtotal", cart_note:"Demo cart — no real payments are processed.",
  cart_checkout:"Checkout", cart_empty:"Your cart is empty.", cart_empty_cta:"Shop the range",
  add:"Add to cart", added:"Added ✓", each:"each", remove:"Remove",
  howto_title:"How to use",
  ship_far:"Add {n} more for <b>free shipping</b>", ship_done:"🎉 You've unlocked <b>free shipping</b>!",
  toast_added:"added to cart", toast_checkout:"Demo store — checkout is disabled.", toast_empty:"Your cart is empty.",
  toast_nl_err:"Please enter a valid email.", toast_nl_ok:"You're in! Demo signup — nothing was actually sent.",
  currency:"SAR",
},
ar:{
  announce:"شحن مجاني للطلبات فوق 150 ر.س ✨",
  nav_home:"الرئيسية", nav_products:"المنتجات", nav_about:"من نحن", nav_faq:"الأسئلة", cart:"السلة",
  settings_title:"الإعدادات", settings_lang:"اللغة", settings_theme:"المظهر", theme_light:"فاتح", theme_dark:"داكن",
  hero_eyebrow:"عناية مشرقة بالشعر",
  hero_title:'شعرٌ يلتقط<br><span class="shine">الضوء</span>.',
  hero_sub:"ثلاثة أساسيات — زيت وبخاخ وكريم — صُنعت لتطويل الشعر وتنعيمه وإشراقه، لكل أنواع الشعر.",
  hero_cta1:"تسوّقي المجموعة", hero_cta2:"قصتنا",
  meta1:"أساسيات يومية", meta2:"سلفات وبارابين", meta3:"صُنع بحب",
  products_eyebrow:"المجموعة", products_title:"ثلاث خطوات<br>لشعرٍ مشرق.",
  products_sub:"روتين متكامل في ثلاثة منتجات. اضغطي على أي منتج لرؤية التفاصيل كاملة.",
  view_details:"عرض التفاصيل",
  ritual_eyebrow:"الروتين", ritual_title:"كيف تستخدمينها معًا",
  step1_t:"فكّي التشابك", step1_p:"رشّي البخاخ على الشعر الرطب أو الجاف ومشّطي بلطف — دون شدّ أو تقصّف.",
  step2_t:"رطّبي", step2_p:"وزّعي كمية صغيرة من الكريم من منتصف الشعر حتى الأطراف لحبس النعومة والترطيب.",
  step3_t:"لمعان ونمو", step3_p:"اختمي ببضع قطرات من الزيت على الأطراف وفروة الرأس لتعزيز الطول والكثافة واللمعان.",
  about_eyebrow:"عن لوميرا", about_title:"اسمها من الضوء.<br>وصُنعت للمعان.",
  about_p1:"«لوميرا» مشتقة من كلمة «lumière» أي الضوء. نؤمن أن الشعر الصحي لا يحتاج رفًّا مليئًا بالمنتجات؛ بل القليل من المنتجات الصادقة التي تعمل فعلًا.",
  about_p2:"لذلك صنعنا ثلاثة فقط: زيت يساعد الشعر على النمو أطول وأكثف، وبخاخ يذيب التشابك، وكريم يحافظ على ترطيب كل خصلة بعمق. لا أكثر ولا أقل.",
  pill1:"نباتي وخالٍ من القسوة", pill2:"لكل أنواع الشعر", pill3:"تركيبات يومية لطيفة",
  reviews_eyebrow:"محبوبة بالفعل", reviews_title:"ماذا يقول أوائل المستخدمين",
  faq_eyebrow:"الأسئلة", faq_title:"كل ما يدور في بالك",
  foot_note:"عناية مشرقة بالشعر في ثلاث خطوات صادقة. متجر تجريبي.",
  foot_shop:"تسوّق", foot_company:"الشركة",
  p1_name:"زيت الشعر", p2_name:"بخاخ فك التشابك", p3_name:"كريم الشعر",
  nl_title:"ابقي في الضوء", nl_sub:"إطلاقات ونصائح وعروض مبكرة. لا رسائل مزعجة أبدًا.",
  nl_ph:"you@email.com", nl_btn:"اشتركي",
  foot_c:"© 2026 لوميرا. موقع تجريبي.", foot_tag:"شعرٌ يلتقط الضوء.",
  cart_title:"سلتك", cart_subtotal:"المجموع", cart_note:"سلة تجريبية — لا تتم أي مدفوعات حقيقية.",
  cart_checkout:"إتمام الشراء", cart_empty:"سلتك فارغة.", cart_empty_cta:"تسوّقي المجموعة",
  add:"أضيفي للسلة", added:"أُضيف ✓", each:"للقطعة", remove:"إزالة",
  howto_title:"طريقة الاستخدام",
  ship_far:"أضيفي {n} لتحصلي على <b>شحن مجاني</b>", ship_done:"🎉 حصلتِ على <b>شحن مجاني</b>!",
  toast_added:"أُضيف إلى السلة:", toast_checkout:"متجر تجريبي — إتمام الشراء معطّل.", toast_empty:"سلتك فارغة.",
  toast_nl_err:"يرجى إدخال بريد إلكتروني صحيح.", toast_nl_ok:"تم الاشتراك! تسجيل تجريبي — لم يُرسل شيء فعليًا.",
  currency:"ر.س",
},
};

/* ============ STATE / HELPERS ============ */
let LANG = "en";
let cart = [];
let modalQty = 1, modalPid = null, lastFocus = null;
const $ = s => document.querySelector(s);
const t = k => I18N[LANG][k] ?? k;
const fmt = n => LANG==="ar" ? `${n} ${t("currency")}` : `${t("currency")} ${n}`;

/* ============ I18N ============ */
function applyLang(lang){
  LANG = lang;
  document.documentElement.lang = lang;
  document.documentElement.dir = lang==="ar" ? "rtl" : "ltr";
  document.querySelectorAll("[data-i18n]").forEach(el=>{ el.innerHTML = t(el.dataset.i18n); });
  document.querySelectorAll("[data-i18n-ph]").forEach(el=>{ el.placeholder = t(el.dataset.i18nPh); });
  $("#heroTitle").innerHTML = t("hero_title");
  $("#langEn").classList.toggle("active", lang==="en");
  $("#langAr").classList.toggle("active", lang==="ar");
  document.title = lang==="ar" ? "لوميرا — عناية بالشعر" : "Luméra — Hair Care";
  renderProducts(); renderReviews(); renderFaqs();
  updateCartUI(false);
  if(modalPid) fillModal(modalPid);
}

/* ============ THEME ============ */
function applyTheme(theme){
  document.documentElement.dataset.theme = theme;
  $("#themeLight").classList.toggle("active", theme==="light");
  $("#themeDark").classList.toggle("active", theme==="dark");
}
$("#themeLight").addEventListener("click", ()=>applyTheme("light"));
$("#themeDark").addEventListener("click", ()=>applyTheme("dark"));
$("#langEn").addEventListener("click", ()=>applyLang("en"));
$("#langAr").addEventListener("click", ()=>applyLang("ar"));

/* settings panel */
const settingsPanel = $("#settingsPanel"), settingsBtn = $("#settingsBtn");
settingsBtn.addEventListener("click", e=>{
  e.stopPropagation();
  const open = settingsPanel.classList.toggle("open");
  settingsBtn.setAttribute("aria-expanded", open);
});
document.addEventListener("click", e=>{
  if(!settingsPanel.contains(e.target) && !settingsBtn.contains(e.target)) settingsPanel.classList.remove("open");
});

/* announcement */
$("#announceClose").addEventListener("click", ()=>{
  $("#announce").classList.add("hidden");
  document.body.classList.remove("announce-on");
});

/* ============ RENDER: PRODUCTS ============ */
function bottleHTML(p, scale=""){
  return `<div class="bottle b-shape ${p.shape}"><span class="b-gloss"></span><span class="b-tag"><i>LUMÉRA</i></span></div>`;
}
const grid = $("#productGrid");
function renderProducts(){
  grid.innerHTML = "";
  PRODUCTS.forEach(p=>{
    const d = p[LANG];
    const card = document.createElement("article");
    card.className = "card reveal in";
    card.innerHTML = `
      <button class="card-stage" data-open="${p.id}" aria-label="${d.name}">
        <span class="num">N°${p.id}</span>
        <span class="view-tag">${t("view_details")}</span>
        <span class="shelf"></span>
        ${bottleHTML(p)}
      </button>
      <div class="card-body">
        <span class="card-benefit">${d.benefit}</span>
        <h3 class="card-name">${d.name}</h3>
        <p class="card-desc">${d.desc}</p>
        <div class="card-foot">
          <span class="price">${fmt(p.price)}</span>
          <button class="add-btn" data-id="${p.id}">${t("add")}</button>
        </div>
      </div>`;
    grid.appendChild(card);
  });
}

/* ============ RENDER: REVIEWS ============ */
function renderReviews(){
  const star = `<svg viewBox="0 0 24 24"><path d="M12 2l3 6.6 7 .8-5.2 4.8 1.4 6.9L12 17.7 5.8 21l1.4-6.9L2 9.4l7-.8z"/></svg>`;
  $("#reviewsGrid").innerHTML = REVIEWS.map(r=>{
    const d = r[LANG];
    return `<div class="review reveal in">
      <div class="stars">${star.repeat(5)}</div>
      <p>"${d.text}"</p>
      <div class="review-who">
        <span class="avatar">${r.init}</span>
        <div><b>${d.name}</b><span>${d.tag}</span></div>
      </div>
    </div>`;
  }).join("");
}

/* ============ RENDER: FAQ ============ */
function renderFaqs(){
  $("#faqList").innerHTML = FAQS.map((f,i)=>{
    const d = f[LANG];
    return `<div class="faq-item">
      <button class="faq-q" aria-expanded="false" data-faq="${i}">
        ${d.q}
        <span class="chev"><svg viewBox="0 0 24 24"><path d="M6 9l6 6 6-6"/></svg></span>
      </button>
      <div class="faq-a"><p>${d.a}</p></div>
    </div>`;
  }).join("");
}
document.addEventListener("click", e=>{
  const q = e.target.closest(".faq-q");
  if(!q) return;
  const item = q.parentElement, a = item.querySelector(".faq-a");
  const open = item.classList.toggle("open");
  q.setAttribute("aria-expanded", open);
  a.style.maxHeight = open ? a.scrollHeight + "px" : 0;
});

/* ============ PRODUCT MODAL ============ */
const modal = $("#modal"), modalCard = $("#modalCard");
function fillModal(pid){
  const p = PRODUCTS.find(x=>x.id===pid), d = p[LANG];
  modalCard.innerHTML = `
    <button class="modal-close" id="modalClose" aria-label="Close">×</button>
    <div class="modal-stage"><span class="shelf"></span>${bottleHTML(p)}</div>
    <div class="modal-info">
      <span class="num" style="font-family:var(--font-display);font-style:italic;font-weight:800;background:var(--grad);-webkit-background-clip:text;background-clip:text;color:transparent">N°${p.id} · ${p.size}</span>
      <span class="card-benefit">${d.benefit}</span>
      <h3>${d.name}</h3>
      <p class="m-desc">${d.desc}</p>
      <ul class="m-features">${d.features.map(f=>`<li>${f}</li>`).join("")}</ul>
      <div class="m-howto"><b>${t("howto_title")}</b>${d.howto}</div>
      <div class="modal-foot">
        <span class="price">${fmt(p.price)}</span>
        <div class="qty">
          <button id="mDec" aria-label="-">−</button>
          <span id="mQty">${modalQty}</span>
          <button id="mInc" aria-label="+">+</button>
        </div>
        <button class="modal-add" id="modalAdd">${t("add")}</button>
      </div>
    </div>`;
  $("#modalClose").addEventListener("click", closeModal);
  $("#mInc").addEventListener("click", ()=>{ modalQty=Math.min(9,modalQty+1); $("#mQty").textContent=modalQty; });
  $("#mDec").addEventListener("click", ()=>{ modalQty=Math.max(1,modalQty-1); $("#mQty").textContent=modalQty; });
  $("#modalAdd").addEventListener("click", e=>{
    addToCart(pid, modalQty, e.currentTarget);
    closeModal();
  });
}
function openModal(pid){
  lastFocus = document.activeElement;
  modalPid = pid; modalQty = 1;
  fillModal(pid);
  modal.classList.add("open"); modal.setAttribute("aria-hidden","false");
  document.body.classList.add("locked");
  $("#modalClose").focus();
}
function closeModal(){
  modal.classList.remove("open"); modal.setAttribute("aria-hidden","true");
  document.body.classList.remove("locked");
  modalPid = null;
  if(lastFocus) lastFocus.focus();
}
modal.addEventListener("click", e=>{ if(e.target===modal) closeModal(); });

/* ============ CART ============ */
const drawer = $("#drawer"), overlay = $("#overlay");
function openCart(){
  lastFocus = document.activeElement;
  drawer.classList.add("open"); overlay.classList.add("open");
  drawer.setAttribute("aria-hidden","false");
  document.body.classList.add("locked");
  $("#cartClose").focus();
}
function closeCart(){
  drawer.classList.remove("open"); overlay.classList.remove("open");
  drawer.setAttribute("aria-hidden","true");
  document.body.classList.remove("locked");
  if(lastFocus) lastFocus.focus();
}
$("#cartOpen").addEventListener("click", openCart);
$("#cartClose").addEventListener("click", closeCart);
overlay.addEventListener("click", closeCart);
document.addEventListener("keydown", e=>{
  if(e.key==="Escape"){ closeCart(); closeModal(); settingsPanel.classList.remove("open"); }
});

function flyToCart(fromEl){
  if(!fromEl || matchMedia("(prefers-reduced-motion:reduce)").matches) return;
  const from = fromEl.getBoundingClientRect();
  const to = $("#cartOpen").getBoundingClientRect();
  const dot = document.createElement("div");
  dot.className = "fly-dot";
  dot.style.left = from.left + from.width/2 + "px";
  dot.style.top = from.top + from.height/2 + "px";
  document.body.appendChild(dot);
  dot.animate([
    {transform:"translate(0,0) scale(1)", opacity:1},
    {transform:`translate(${to.left+to.width/2-(from.left+from.width/2)}px,${to.top+to.height/2-(from.top+from.height/2)}px) scale(.4)`, opacity:.6}
  ],{duration:600,easing:"cubic-bezier(.2,.7,.3,1)"}).onfinish = ()=>dot.remove();
}

function addToCart(pid, qty, sourceEl){
  const p = PRODUCTS.find(x=>x.id===pid);
  const line = cart.find(x=>x.id===pid);
  line ? line.qty += qty : cart.push({id:pid, price:p.price, qty});
  flyToCart(sourceEl);
  updateCartUI();
  showToast(LANG==="ar" ? `${t("toast_added")} ${p.ar.name}` : `${p.en.name} ${t("toast_added")}`);
}

function updateCartUI(pop=true){
  const count = cart.reduce((s,i)=>s+i.qty,0);
  const total = cart.reduce((s,i)=>s+i.price*i.qty,0);
  const badge = $("#cartCount");
  badge.textContent = count;
  badge.classList.toggle("zero", count===0);
  if(pop && count){ badge.classList.add("pop"); setTimeout(()=>badge.classList.remove("pop"),200); }

  /* free shipping bar */
  const pct = Math.min(100, total/FREE_SHIP*100);
  $("#shipFill").style.width = pct + "%";
  $("#shipMsg").innerHTML = total >= FREE_SHIP
    ? t("ship_done")
    : t("ship_far").replace("{n}", fmt(FREE_SHIP - total));

  const box = $("#cartItems");
  if(!cart.length){
    box.innerHTML = `<div class="cart-empty"><span>${t("cart_empty")}</span>
      <button class="btn btn-solid" style="border:none" id="emptyCta">${t("cart_empty_cta")}</button></div>`;
    $("#emptyCta").addEventListener("click", ()=>{ closeCart(); document.querySelector("#products").scrollIntoView({behavior:"smooth"}); });
  } else {
    box.innerHTML = cart.map(i=>{
      const d = PRODUCTS.find(p=>p.id===i.id)[LANG];
      return `
      <div class="cart-item">
        <div class="cart-thumb"><i>N°${i.id}</i></div>
        <div class="cart-item-info">
          <b>${d.name}</b>
          <span>${fmt(i.price)} ${t("each")} · ${fmt(i.price*i.qty)}</span><br>
          <button class="remove-btn" data-remove="${i.id}">${t("remove")}</button>
        </div>
        <div class="qty">
          <button data-dec="${i.id}" aria-label="-">−</button>
          <span>${i.qty}</span>
          <button data-inc="${i.id}" aria-label="+">+</button>
        </div>
      </div>`;}).join("");
  }
  $("#subtotal").textContent = fmt(total);
}

document.addEventListener("click", e=>{
  const stage = e.target.closest("[data-open]");
  if(stage){ openModal(+stage.dataset.open); return; }
  const add = e.target.closest(".add-btn");
  if(add){
    addToCart(+add.dataset.id, 1, add);
    add.textContent = t("added"); add.classList.add("added");
    setTimeout(()=>{ add.textContent=t("add"); add.classList.remove("added"); },1200);
  }
  if(e.target.dataset.inc){ cart.find(x=>x.id==e.target.dataset.inc).qty++; updateCartUI(); }
  if(e.target.dataset.dec){
    const l = cart.find(x=>x.id==e.target.dataset.dec);
    l.qty--; if(l.qty<1) cart = cart.filter(x=>x!==l);
    updateCartUI();
  }
  if(e.target.dataset.remove){ cart = cart.filter(x=>x.id!=e.target.dataset.remove); updateCartUI(); }
});

$("#checkoutBtn").addEventListener("click", ()=>{
  showToast(cart.length ? t("toast_checkout") : t("toast_empty"));
});

/* ============ NEWSLETTER (demo) ============ */
$("#nlBtn").addEventListener("click", ()=>{
  const v = $("#nlEmail").value;
  if(!v.includes("@") || !v.includes(".")){ showToast(t("toast_nl_err")); return; }
  $("#nlEmail").value = "";
  showToast(t("toast_nl_ok"));
});

/* ============ TOAST ============ */
let toastTimer;
function showToast(msg){
  const el = $("#toast");
  el.textContent = msg;
  el.classList.add("show");
  clearTimeout(toastTimer);
  toastTimer = setTimeout(()=>el.classList.remove("show"),2400);
}

/* ============ NAV: scroll, spy, progress, top ============ */
const nav = $("#nav");
const spyLinks = [...document.querySelectorAll("[data-spy]")];
const spySections = spyLinks.map(a=>document.getElementById(a.dataset.spy));
addEventListener("scroll", ()=>{
  nav.classList.toggle("scrolled", scrollY>10);
  /* progress */
  const h = document.documentElement;
  const pct = h.scrollTop / (h.scrollHeight - h.clientHeight) * 100;
  $("#progress").style.width = pct + "%";
  /* back to top */
  $("#toTop").classList.toggle("show", scrollY > innerHeight * .8);
  /* scrollspy */
  let current = "home";
  spySections.forEach(sec=>{ if(sec && sec.getBoundingClientRect().top < innerHeight*.4) current = sec.id; });
  spyLinks.forEach(a=>a.classList.toggle("active", a.dataset.spy===current));
},{passive:true});
$("#toTop").addEventListener("click", ()=>scrollTo({top:0,behavior:"smooth"}));

const menuBtn = $("#menuBtn"), navLinks = $("#navLinks");
menuBtn.addEventListener("click", ()=>{
  const open = navLinks.classList.toggle("open");
  menuBtn.classList.toggle("open", open);
  menuBtn.setAttribute("aria-expanded", open);
});
navLinks.addEventListener("click", e=>{
  if(e.target.tagName==="A"){ navLinks.classList.remove("open"); menuBtn.classList.remove("open"); }
});

/* ============ SCROLL REVEAL ============ */
const io = new IntersectionObserver(entries=>{
  entries.forEach(en=>{ if(en.isIntersecting){ en.target.classList.add("in"); io.unobserve(en.target); }});
},{threshold:.12});
document.querySelectorAll(".reveal").forEach(el=>io.observe(el));

/* ============ INIT ============ */
applyLang("en");
applyTheme(matchMedia("(prefers-color-scheme:dark)").matches ? "dark" : "light");
</script>
</body>
</html>
