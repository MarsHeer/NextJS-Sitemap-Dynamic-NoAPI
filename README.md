# NextJS-Sitemap-Dynamic-NoAPI
Add a dynamic sitemap to your site, without APIs or dependencies.

# Change domain
Remember to input your domain into the "domain" variable.

# Use in pages
To be able to access your sitemap from "www.yourdomain.com/Sitemap.xml" and for the script to work, save it in the "pages" folder.


````
import React from 'react';

import { Pages } from '../components/PageList';

let today = new Date();
let date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
const domain = 'https://domain.com/';

const sitemapXml = () => {
    
    let xml = `<?xml version="1.0" encoding="UTF-8"?>
    <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
    <loc>` + domain + `</loc>
    <lastmod>` + date + `</lastmod>
    </url>`;

    Object.keys(Streamers).map((key) => {
        let push = `<url>
        <loc>` + domain + `page/` + key + `</loc>
        <lastmod>` + date + `</lastmod>
        </url>`;
        xml += push;
    })

    xml += `</urlset>`;

    return xml;
}

class Sitemap extends React.Component {
  static async getInitialProps({ res }) {
    res.setHeader("Content-Type", "text/xml");
    res.write(sitemapXml());
    res.end();
  }
}

export default Sitemap;
````

