This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Servidor (VPS)

No se despliega en Vercel: corre en el VPS de Irida con Docker Compose, detrás de nginx (contenedor
`strongwood_ventas_next`). Cómo se despliega y las reglas del servidor están en la
[guía del VPS](https://github.com/IridaStudio/vps/blob/master/README.md) (repo `IridaStudio/vps`); acá no se copian.
Lo que más importa al tocar este repo:

- **La imagen se arma en la PC, nunca en el VPS:** `bash vps/scripts/desplegar.sh strongwood-ventas` desde la carpeta
  `iridastudio` ([Cómo desplegar](https://github.com/IridaStudio/vps/blob/master/README.md#cómo-desplegar)). Si cambia
  solo el `docker-compose.yml`, no hace falta armar imagen
  ([Si cambia solo el compose](https://github.com/IridaStudio/vps/blob/master/README.md#si-cambia-solo-el-compose)).
- **Tope de memoria:** el `mem_limit` de 512 MB del compose es regla del servidor: no se saca ni se cambia sin decidirlo
  en la guía ([Topes de memoria](https://github.com/IridaStudio/vps/blob/master/README.md#topes-de-memoria)). Hoy usa
  unos 50-170 MB.
- **La receta de imágenes:** solo WebP y `deviceSizes` hasta 1920 en `next.config.ts`, y la caché de `/_next/image` en
  el volumen `strongwood-ventas-image-cache`. Es la receta que copiaron las otras webs con fotos: con AVIF la memoria
  crecía sin parar. No volver a poner AVIF.
