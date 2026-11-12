# ProxyGosha — Telegram WEB Proxy on Cloudflare Workers

> A private Telegram proxy on Cloudflare's free plan. One file, one setting, no server.

<p align="center">
  <a href="https://github.com/amirmarandidev/ProxyGosha/stargazers"><img src="https://img.shields.io/github/stars/amirmarandidev/ProxyGosha?style=for-the-badge&color=gold" alt="GitHub Stars"></a>
  <a href="https://workers.cloudflare.com/"><img src="https://img.shields.io/badge/Cloudflare-Workers-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudflare Workers"></a>
  <a href="https://desktop.telegram.org/"><img src="https://img.shields.io/badge/Telegram-WEB%20Proxy-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram WEB Proxy"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License MIT"></a>
</p>

<p align="center">
  <a href="README.md"><b>English</b></a> •
  <a href="docs/README.fa.md"><b>فارسی</b></a> •
  <a href="docs/README.ru.md"><b>Русский</b></a> •
  <a href="docs/README.zh.md"><b>简体中文</b></a> •
  <a href="docs/llms.txt"><b>llms.txt</b></a>
</p>

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ali-master/tg-proxy)

Telegram's **WEB** proxy type travels as ordinary HTTPS, so it can run on Cloudflare. ProxyGosha turns a free Worker into one. Visitors see an online store; Telegram traffic stays end-to-end encrypted, so the proxy cannot read it.

## Quick start

1. **Deploy.** Click the button above, sign in, and set `ADMIN_KEY` to a random password of 16+ letters and digits.
   *Manual:* paste [`worker.js`](worker.js) into a new Worker in the [dashboard](https://dash.cloudflare.com/), then add `ADMIN_KEY` under **Settings → Variables and Secrets**.
2. **Add a custom domain.** Worker → **Settings → Domains & Routes → Custom Domain** (for example `tg.yourdomain.com`). `workers.dev` is filtered in Iran, China and Russia.
3. **Connect.** Open `https://tg.yourdomain.com/<ADMIN_KEY>` and tap **Connect in Telegram**.

Share only the links, never the panel address. Live stats and a Telegram DC probe are at `/<ADMIN_KEY>/status`.

## Settings

| Variable | Purpose |
|---|---|
| `ADMIN_KEY` | **Required.** Panel password; secrets are derived from it. |
| `SECRET` | Fixed 32-hex secret. Set it so changing `ADMIN_KEY` does not break shared links. |
| `EXTRA_HOSTS` | More domains on this Worker, comma separated. |
| `DECOY_URL` | Real site to show visitors instead of the built-in store. |
| `CARRIER` | Leave empty; `websocket` only if the default misbehaves. |
| `UPSTREAM` | Leave empty (Telegram's WebSocket servers, TCP fallback); `tcp` for raw TCP only. |

## If it does not connect

- Try another port: `443` `2053` `2083` `2087` `2096` `8443` (each has its own secret in the panel).
- Attach another domain and add it to `EXTRA_HOSTS`.
- Desktop: map your domain to a working Cloudflare IP in your `hosts` file.
- Russia: turn off **ECH** under **SSL/TLS → Edge Certificates**.
- See what happens: Cloudflare → your Worker → **Logs**. Each `[tgproxy] stream_end` line shows the DC, the path (TCP or kws), connect time, bytes and why the connection closed. If you pasted the code by hand, first turn on **Settings → Observability → Workers Logs**.

Step-by-step guides with screenshots and FAQ: [فارسی](docs/README.fa.md) · [Русский](docs/README.ru.md) · [简体中文](docs/README.zh.md) · [Video](https://youtu.be/7StSCQdpqvk)

## Community & support

[Telegram channel](https://t.me/amirdotlog) · [YouTube](https://www.youtube.com/@amirmarandidev)

Donate — **USDT (BEP20):** `0xd593ae9D32bEA690EC62460C54BF3951aFFF7803` · **USDT (TRC20):** `THaaHzoTwXfUfcrtYTDXRsMmk9qhnXa56M`

> [!NOTE]
> For education and personal use. Running proxies on Workers may conflict with Cloudflare's Terms of Service (2.2.1(j)). You are responsible for how you use it.
