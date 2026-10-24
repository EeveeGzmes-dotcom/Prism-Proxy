# Prism Proxy

A small web proxy built on Ultraviolet, with an Epoxy transport that tunnels through a Wisp server:

    wss://bare-server.fly.dev/wisp/

## Run it

    npm install
    npm start

Then open http://localhost:8080 (set `PORT` to change it).

Service workers only run on `localhost` or HTTPS, so if you deploy this, put it behind HTTPS.

## Layout

    server.js              Express server; mounts Ultraviolet, Epoxy and bare-mux assets
    public/index.html      UI, registers the service worker and sets the Wisp transport
    public/sw.js           Ultraviolet service worker
    public/uv/uv.config.js Ultraviolet config (URL prefix /service/, XOR codec)

## Change the Wisp server

Edit `WISP_URL` near the top of the script in `public/index.html`.

## Notes

- This was written without being installed or run, so expect to fix small version differences
  in the `@titaniumnetwork-dev/ultraviolet`, `@mercuryworkshop/bare-mux` and
  `@mercuryworkshop/epoxy-transport` packages if their APIs have changed.
- The Wisp server belongs to a third party and sees the hostnames and traffic you send through it.
  Avoid logging in to sensitive accounts through it.
- Some sites (heavy web apps, anything with strict anti-bot checks) won't work through any web proxy.
