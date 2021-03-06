<img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"><img src="https://img.shields.io/badge/html-E34F26?style=for-the-badge&logo=html5&logoColor=white"><img src="https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=black"><img src="https://img.shields.io/badge/React Router-CA4245?style=for-the-badge&logo=React Router&logoColor=black"><img src="https://img.shields.io/badge/styled components-DB7093?style=for-the-badge&logo=styled-components&logoColor=white"><img src="https://img.shields.io/badge/Redux-764ABC?style=for-the-badge&logo=Redux&logoColor=white">



# ๐ฌ Switter 
### ํ๋ก์ ํธ ์ค๋ช
* React์ Firebase๋ฅผ ์ฌ์ฉํ Twitter (mini)Clone
* ์ฝ๋ก๋ ํํฉ์ ์ํ ์ธ๋ถ๊ณต๊ณต๋ฐ์ดํฐ API ์ฌ์ฉ
* ์ต์  ์ธ๊ธฐ ๋์์ ๊ฒ์์ ์ํ kakao API๋ฅผ ์ฌ์ฉ

### ๊ฐ ๋ถ๋ถ ๊ตฌํ๋ ์ด๋ฏธ์ง์ ๊ตฌํ์ ์ฌ์ฉํ ๋ฐฉ์๊ณผ ๋ผ์ด๋ธ๋ฌ๋ฆฌ
1. ๋ก๊ทธ์ธ / ๋ฉ์ธ / ํ๋กํ / ๋ก๊ทธ์์
* ๊ธฐ๋ณธ ๋ก๊ทธ์ธ/ํ์๊ฐ์ ๋ฐ ์์ ์ธ์ฆ์ ํตํ ๋ก๊ทธ์ธ
* ๊ธ ์๋ ฅ๊ณผ ์ด๋ฏธ์ง ์ฒจ๋ถ
* ํด๋น ์ ์ ๊ฐ ์์ฑํ ๊ธ์ ๋ํด์๋ง ์์ /์ญ์  ๊ฐ๋ฅ
* ํด๋น ์ ์ ์ displayName์ ์ด์ฉํ์ฌ ํ๋กํ๋ช ๋ณ๊ฒฝ ๊ฐ๋ฅ 
* ๋ก๊ทธ์์

![๋ก๊ทธ์ธ](https://user-images.githubusercontent.com/74355328/146699283-13a7381f-49e4-4069-80c2-1ed5046fd8bf.gif)

2. ์ฝ๋ก๋ 

![corona](https://user-images.githubusercontent.com/74355328/146196626-114d1872-d5c5-4060-b6a5-c6e52e6131ec.gif)

* ์ฝ๋ก๋์ ์ ์ฒด์ ์ธ ๊ฐ์ผ ์ ๋ณด ํ์
* ์ฝ๋ก๋์ ์ง์ญ๋ณ ๊ฐ์ผ ์ ๋ณด ํ์
  * svg ์ ๊ตญ ์ง๋๋ฅผ react์์ ์ฌ์ฉํ๊ธฐ ์ํด file-loader ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ค์น
  ```javascript
  npm install file-loader --save-dev
  ```
   * node_modules/react-scripts/config/webpack.config.js์์ svg๋ฅผ ์ฝ์ ์ ์๋ ์ฝ๋ ์ถ๊ฐ
  ```javascript
  {
    test: /\.(png|jp(e*)g|svg|gif)$/,
    use: [
      {
        loader: 'file-loader',
        options: {
          name: 'images/[hash]-[name].[ext]',
        },
      },
    ],
  },
  ```
   * ๋ง์ฐ์ค ์ค๋ฒ๋๋ ์ง์ญ์ ์ฝ๋ก๋ ๊ฐ์ผ ์ ๋ณด๋ฅผ ๋ํ๋ด๋ ํดํ์ getScreenCTM() ํจ์๋ฅผ ์ฌ์ฉํด์ ๊ตฌํ
  ```javascript
  const mouseOverHandler = (e) => {
        //e.target์ ์ฌ์ฉํ  ๊ฒฝ์ฐ ๋ฒ๋ธ๋ง์ผ๋ก ์ด๋ฒคํธ๊ฐ ํ์์์์ ๊ฐ๊ฐ ๋ฐ์ํจ
        //--> ๊ทธ๋ฃน ์์์ ํด๋์ค ์ญ์  ์ถ๊ฐ๋  ์ ์๋๋ก e.currentTarget ์ฌ์ฉ 
        e.currentTarget.classList.add('city_hover')

        //ํดํ์ ์์น ๊ณ์ฐํ๊ธฐ
        const CTM = svg.getScreenCTM()
       
        tooltip.setAttributeNS(null, "visibility", "visible")

        //ํ์คํธ ๋ณ๊ฒฝํ๊ธฐ
        const info = sidoCovidInfo.find((item, index) => index === e.currentTarget.tabIndex)
        const { deathCnt, defCnt, gubun } = info
        e.currentTarget.setAttributeNS(null, "data-text", `${gubun}/ํ์ง์:${defCnt}๋ช/์ฌ๋ง์:${deathCnt}๋ช`)

        //๋ฐฐ๊ฒฝ ๋ง๋ค๊ธฐ
        //๋ฐฐ๊ฒฝ ์์น๋ transform์ผ๋ก ์ค์  
        const x = (e.clientX - CTM.e + 6) / CTM.a
        const y = (e.clientY - CTM.f + 20) / CTM.d
        tooltip.setAttributeNS(null, "transform", `translate(${x}, ${y})`)

        const tooltipText = tooltip.getElementsByTagName('text')[0]
        tooltipText.firstChild.data = e.currentTarget.getAttributeNS(null, "data-text");
        
        //ํดํ ๊ธธ์ด ๋ณ๊ฒฝ 
        const tooltipRects = tooltip.getElementsByTagName('rect')
        const length = tooltipText.getComputedTextLength()//ํ์คํธ ์์์ ๊ธธ์ด ๊ตฌํ๊ธฐ
        for (let i = 0; i < tooltipRects.length; i++) {//ํ์คํธ ๊ธธ์ด์ ๋ง๊ฒ ๋์ด ๋ณ๊ฒฝ
            tooltipRects[i].setAttributeNS(null, "width", length + 8);
        }    
    }
   ```

3. ๋์์ ๊ฒ์

![๋์์๊ฒ์](https://user-images.githubusercontent.com/74355328/146197013-2a2114a7-6d68-43b6-9293-029bf265dccc.gif)

* ์๋ ฅ๋ ๊ฒ์์ด์ ๋ฐ๋ฅธ ์ธ๊ธฐ ๋์์์ kaka API๋ฅผ ์ฌ์ฉํ์ฌ ํ์

### ๊ตฌํํ๋ฉด์ ์ด๋ ค์ ๋ ์ 
* ์ธ๋ถ๊ณต๊ณต๋ฐ์ดํฐ API๋ฅผ ์ฌ์ฉํ๋ ค๋๋ฐ ๋ธ๋ผ์ฐ์ ๊ฐ ๋ณด์์ ์ํด ๊ต์ฐจ ์ถ์ฒ ๋ฆฌ์์ค ๊ณต์ ๋ฅผ ์ ํ
  * ํด๊ฒฐ: ๋ฌด๋ฃ ๋ธ๋ฆฌ์ง ํด๋ผ์ฐ๋ ์๋น์ค๋ฅผ ์ด์ฉ
  ```javascript
  const response = await axios.get(`https://cors.bridged.cc/http://openapi.data.go.kr/...`, {
                    headers: {
                        'x-cors-grida-api-key': 'myapikey',
                        'Content-Type': 'application/json'
                    }
                })
  ```
  * ์ฐธ๊ณ ( https://github.com/gridaco/base/issues/23)
* svg๋ฅผ react์ ์ง์  ์ฌ์ฉํ๋ ๋ถ๋ถ
  * ํด๊ฒฐ: webpack.config.js์ ์ฝ๋ ์ถ๊ฐ
  * ๊ทธ ์ธ์๋ svg ํ์ผ๋ก ์ ์ฅํ๊ณ , ๋ถ๋ฌ์์ img ํ๊ทธ์ ์์ฑ๊ฐ์ ๋ฃ์ด ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ๊ณผ ๋ถ๋ฌ์์ svg๋ฅผ ์ปดํฌ๋ํธ์ฒ๋ผ ์ฌ์ฉ๋ ๋ฐฉ๋ฒ๋ ์๊ฒ๋จ
  * webpack์ด ์ด๋ค ์ญํ ์ ํ๋์ง ๊ณต๋ถํ  ์ ์๋ ์ข์ ๊ณ๊ธฐ๊ฐ ๋จ
* ํดํ ๊ตฌํ
  * https://www.petercollingridge.co.uk/tutorials/svg/interactive/tooltip/ ํด๋น ์ฌ์ดํธ๋ฅผ ์ฐธ๊ณ ํ์ฌ ๊ตฌํ
