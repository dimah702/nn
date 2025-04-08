# nn
{
  "name": "sena-store-v2",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.0.0",
    "vite": "^4.0.0"
  }
}
<!DOCTYPE html>
<html lang="ar" dir="rtl">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>سِنا</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})
import React from 'react'
import ReactDOM from 'react-dom/client'
import SenaStore from './SenaStore'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <SenaStore />
  </React.StrictMode>
)
import React from "react";

// الفئات:
// 1. بلوفرات عاديه (Plain)
// 2. بلوفرات مزخرفه (Patterned)

// أسماء البلوفرات العادية:
const plainNames = ["نَدى", "صَفا", "وَرد", "كُحل", "طين", "ضَحى", "ليل", "غيم"];

// أسماء البلوفرات المزخرفة:
const patternedNames = ["سَما", "رَمل", "غَسق", "زَهر"];

const categories = [
  { title: "بلوفرات عاديه", key: "plain" },
  { title: "بلوفرات مزخرفه", key: "patterned" },
];

const sizes = ["XS", "S", "M", "L", "XL", "2XL"];

// إنشاء المنتجات لكل فئة
const products = {
  // لكل بلوفر عادي، نستخدم اسم من القائمة، والصورة عبارة عن رابط placeholder مع الاسم
  plain: plainNames.map((name) => ({
    image: `https://via.placeholder.com/300x400?text=${encodeURIComponent(name)}`,
    name: `بلوفر ${name}`
  })),
  // لكل بلوفر مزخرف نستخدم الاسم المناسب؛ صورة placeholder مع الاسم بدون تغيير كلمة "سِنا" عليها (حيث تكتب "سِنا" في زاوية الصورة لاحقاً بالتصميم)
  patterned: patternedNames.map((name) => ({
    image: `https://via.placeholder.com/300x400?text=${encodeURIComponent(name)}`,
    name: `بلوفر ${name}`
  })),
};

export default function SenaStore() {
  return (
    <div style={{ padding: 24, fontFamily: 'sans-serif' }}>
      <header style={{ textAlign: 'center', marginBottom: 40 }}>
        <h1 style={{ fontSize: 32 }}>سِنا</h1>
        <p style={{ maxWidth: 600, margin: '0 auto', lineHeight: 1.6 }}>
          في “سِنا”، نصمم بلوفرات بألوان مدروسة بعناية لتناسب الأشخاص المصابين بعمى الألوان، خاصة عمى الأحمر والأخضر.
          نؤمن بأن الأناقة يجب أن تكون متاحة للجميع، لذلك اخترنا ألوانًا يسهل تمييزها، دون أن نفقد لمستنا الجمالية.
          <br /><br />
          استلهمنا اسمنا وهويتنا من الجمال العربي، وأضافنا لمسات تراثية في التصميم والخطوط المستخدمة لتكون كل قطعة ليست فقط مريحة وأنيقة، بل تحكي قصة.
        </p>
      </header>

      {categories.map(({ title, key }) => (
        <section key={key} style={{ marginBottom: 48 }}>
          <h2 style={{ fontSize: 24, marginBottom: 16 }}>{title}</h2>
          <div
            style={{
              display: "grid",
              gridTemplateColumns: "repeat(auto-fit, minmax(200px, 1fr))",
              gap: 16,
            }}
          >
            {products[key].map((product, index) => (
              <div
                key={index}
                style={{ border: "1px solid #ddd", borderRadius: 8, overflow: "hidden" }}
              >
                <div style={{ position: "relative" }}>
                  <img
                    src={product.image}
                    alt={product.name}
                    style={{ width: "100%", height: 250, objectFit: "cover" }}
                  />
                  {/* نص "سِنا" بخط صغير في زاوية الصورة */}
                  <div
                    style={{
                      position: "absolute",
                      top: 8,
                      right: 8,
                      backgroundColor: "rgba(255, 255, 255, 0.7)",
                      padding: "2px 6px",
                      fontSize: 12,
                      borderRadius: 4,
                    }}
                  >
                    سِنا
                  </div>
                </div>
                <div style={{ padding: 12 }}>
                  <h3 style={{ margin: "8px 0", fontWeight: "bold" }}>{product.name}</h3>
                  <div style={{ display: "flex", flexWrap: "wrap", gap: 6 }}>
                    {sizes.map((size) => (
                      <span
                        key={size}
                        style={{
                          border: "1px solid #ccc",
                          padding: "4px 8px",
                          borderRadius: 4,
                          fontSize: 12,
                        }}
                      >
                        {size}
                      </span>
                    ))}
                  </div>
                  <button
                    style={{
                      marginTop: 10,
                      width: "100%",
                      padding: 8,
                      backgroundColor: "#111",
                      color: "#fff",
                      border: "none",
                      borderRadius: 4,
                      cursor: "pointer",
                    }}
                  >
                    أضف إلى السلة
                  </button>
                </div>
              </div>
            ))}
          </div>
        </section>
      ))}
    </div>
  );
}
