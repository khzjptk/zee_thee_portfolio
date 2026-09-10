# Zee Thee Digital — Website

Static landing page. Build step မလိုပါ။ ဖိုင်တွေကို တင်လိုက်ရုံပါပဲ။

```
web/
  index.html          ← စာမျက်နှာ တစ်ခုလုံး (CSS + JS အတွင်းမှာ ပါပြီး)
  logo.png            ← လုံးဝ lockup (footer)
  logo-mark.png       ← ဇီးသီး mark (nav, avatar)
  favicon-32.png
  apple-touch-icon.png
  og.png              ← Facebook / Telegram share preview (1200×630)
  _headers            ← Cloudflare Pages security headers
  robots.txt
```

Logo assets များကို `~/Documents/zeethee.jpg` မှ background ဖြုတ်၍ ထုတ်ထားသည်။

## ⚠️ VPN server ပေါ်မှာ မတင်ပါနှင့်

Outline customer traffic က port `443` ကို သုံးနေပြီး၊ website ကလည်း `443` လိုသည် — port conflict ဖြစ်မည်။
ပိုအရေးကြီးသည်မှာ public website တင်လိုက်လျှင် **VPN server ၏ IP ပေါ်သွားပြီး block ခံရနိုင်သည်**။
Website ကို Cloudflare Pages သို့မဟုတ် သီးခြား VPS တွင်သာ ထားပါ။

## Deploy — Cloudflare Pages

### နည်းလမ်း ၁ · Git (အကြံပြု)

1. [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. `khzjptk/tg_bot_test` repo ကို ရွေးပါ
3. Build settings —
   - Framework preset: **None**
   - Build command: *(အလွတ်ထားပါ)*
   - Build output directory: `web`
4. **Save and Deploy**

`main` သို့ push တိုင်း အလိုအလျောက် deploy ဖြစ်သွားပါမည်။

### နည်းလမ်း ၂ · တိုက်ရိုက် တင်ခြင်း

Pages → **Upload assets** → `web/` ဖိုလ်ဒါကို drag & drop လုပ်ပါ။

## Domain — `zeetheedigital.online`

Domain ကို index.html, robots.txt, sitemap.xml အားလုံးမှာ ထည့်ပြီးပါပြီ။
Cloudflare Pages မှာ ချိတ်ရန် —

1. Pages project → **Custom domains** → **Set up a domain**
2. `zeetheedigital.online` နှင့် `www.zeetheedigital.online` နှစ်ခုလုံး ထည့်ပါ
3. Cloudflare ပြသည့် DNS record ကို ထည့်ပါ — HTTPS certificate က မိနစ်အနည်းငယ်အတွင်း အလိုအလျောက် ရပါမည်

## SEO

| ပါဝင်သည် | မှတ်ချက် |
|---|---|
| `sitemap.xml` · `robots.txt` | Domain ထည့်ပြီးသား |
| Canonical + hreflang (`my`, `x-default`) | |
| Open Graph + Twitter Card | `og.png` 1200×630 — Facebook/Telegram share preview |
| JSON-LD `Organization` | Logo, Facebook page, Telegram channel, support contact |
| JSON-LD `WebSite` | `inLanguage: my` |
| JSON-LD `Product` × 2 | Zee Plus / Zee Max — MMK offer ၄ ခု |
| JSON-LD `FAQPage` | FAQ ၈ ခု — Google search result မှာ တိုက်ရိုက် ပေါ်နိုင်သည် |

Deploy ပြီးလျှင် —

1. [Google Search Console](https://search.google.com/search-console) မှာ domain ထည့်ပြီး
   `https://zeetheedigital.online/sitemap.xml` ကို submit လုပ်ပါ
2. [Rich Results Test](https://search.google.com/test/rich-results) နှင့် JSON-LD ကို စစ်ပါ
3. [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) မှာ og image ကို refresh လုပ်ပါ

**FAQ ပြင်လျှင်** — `index.html` ထဲက `<details>` များနှင့် JSON-LD `FAQPage` နှစ်ခုလုံး တူညီရမည်။

## Local မှာ ကြည့်ရန်

```bash
cd web && python3 -m http.server 8080
# http://localhost:8080
```

## ဈေးနှုန်း ပြင်ရန်

ဈေးနှုန်းများကို `index.html` ထဲမှာ တိုက်ရိုက် ရေးထားသည်။ Bot database (`package_prices`) မှာ
ပြောင်းလိုက်လျှင် ဤနေရာလည်း လက်ဖြင့် ပြင်ရမည် —

| နေရာ | တန်ဖိုး |
|---|---|
| `data-p1` / `data-p3` (Zee Basic) | `3,000` / `9,000` |
| `data-p1` / `data-p3` (Zee Plus)  | `7,000` / `20,000` |
| `data-p1` / `data-p3` (Zee Max)   | `18,000` / `52,000` |
| `data-save` (Zee Plus / Zee Max)  | `1,000` / `2,000` MMK သက်သာ |

JSON-LD `Offer` သုံးစုံကိုပါ လိုက်ပြင်ရမည် — Google က ဤနေရာကို ဖတ်သည်။

## မထည့်ရန် (BOT_TEXTS.md စည်းကမ်း)

- ငွေပြန်အမ်းမည် ကတိ
- Speed အာမခံချက်
- Server IP / hostname, Outline API အချက်အလက်
- Region တစ်ခုစီမှာ server ဘယ်နှစ်လုံးရှိသည်ဆိုသော အရေအတွက်

> Region **နာမည်** (Singapore, Japan) ကတော့ 2026-09-10 မှစ၍ owner ဆုံးဖြတ်ချက်အရ
> ရောင်းအားအတွက် ဖော်ပြသည် — `#regions` section နှင့် plan card တိုင်းတွင် ပါသည်။
> ဖော်ပြရမည်မှာ region နာမည်နှင့် ရွေးချယ်နိုင်ကြောင်းသာ; server အရေအတွက်နှင့်
> လိပ်စာများ မဟုတ်ပါ။

## Hosting

Cloudflare Pages / Workers static assets မှ တင်သည်။ Build step မရှိပါ —
repo ၏ root ကို တိုက်ရိုက် တင်သည် (`Build command` ဗလာ, `Root directory` `/`)။

- `_headers` — security header များ။ Cloudflare က ဖတ်ပြီး serve မလုပ်ပါ။
- `.assetsignore` — `.git` စသည်တို့ကို မတင်စေရန်။ **ဖျက်၍ မရပါ** — မရှိလျှင်
  `.git` directory တစ်ခုလုံး public ဖြစ်ပြီး repo history အားလုံး
  ဆွဲထုတ်၍ ရသွားသည် (2026-09-07 တွင် တကယ် ဖြစ်ခဲ့ပြီး ပြင်ပြီး)။

**Server ပေါ်တွင် self-host မလုပ်ပါနှင့်** — အထူးသဖြင့် Outline VPN node ပေါ်တွင်
container တင်လျှင် ထို node ၏ VPN key များ ရပ်သွားသည်။ အသေးစိတ်ကို
`ServerDeploy/step_3.md` တွင် ကြည့်ပါ။
