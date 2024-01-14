# OpenAI DALL-E를 이용한 이미지 생성 사이트

이 웹사이트는 OpenAI의 DALL-E 기술을 활용하여 사용자가 입력한 텍스트 프롬프트에 기반한 맞춤형 이미지를 생성하는 플랫폼입니다. 사용자는 원하는 텍스트를 입력하고, DALL-E가 그에 맞는 독창적이고 창의적인 이미지를 생성하는 경험을 할 수 있습니다.
[참고영상](https://www.youtube.com/watch?v=EyIvuigqDoA&list=PLpwSgcyFeRw3jKpo_WtvrIl9CFSwXNe9R&index=3&t=11s)

## 제작기간

2024-01-13 시작
~ 2024-01-14 완료

## 완성작 보기

미리보기 :

<div align=center>
<img width=100% src="![image](https://github.com/audgns722/dall-e-clone-vitereact/assets/144664895/a706f899-49df-41bb-bf65-950b2b09f4b7)
">
</div>

## 프로젝트 구성

<details>
<summary>📦client</summary>

```
 ┣ 📂public
 ┃ ┗ 📜vite.svg
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📜Card.jsx
 ┃ ┃ ┣ 📜FormField.jsx
 ┃ ┃ ┣ 📜index.js
 ┃ ┃ ┗ 📜Loader.jsx
 ┃ ┣ 📂constant
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂pages
 ┃ ┃ ┣ 📜CreatePost.jsx
 ┃ ┃ ┣ 📜Home.jsx
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📂utils
 ┃ ┃ ┗ 📜index.js
 ┃ ┣ 📜App.css
 ┃ ┣ 📜App.jsx
 ┃ ┣ 📜index.css
 ┃ ┗ 📜main.jsx
 ┣ 📜.eslintrc.cjs
 ┣ 📜index.html
 ┣ 📜package-lock.json
 ┣ 📜package.json
 ┣ 📜postcss.config.js
 ┣ 📜tailwind.config.js
 ┗ 📜vite.config.js
```

</details>

<details>
<summary>📦server</summary>

```
 ┣ 📂mongodb
 ┃ ┣ 📂models
 ┃ ┃ ┗ 📜post.js
 ┃ ┗ 📜connect.js
 ┣ 📂routes
 ┃ ┣ 📜dalleRoutes.js
 ┃ ┗ 📜postRoutes.js
 ┣ 📜.env
 ┣ 📜index.js
 ┣ 📜package-lock.json
 ┗ 📜package.json
```

</details>

## 라이브러리 및 기술 스택

### 클라이언트(Client)

React, Vite, Tailwind CSS, PostCSS, React Router, axios

### 서버(Server)

Node.js, Express, Mongoose, MongoDB, dotenv, CORS, Nodemon, OpenAI, Cloudinary

### client

```
npm create vite@latest
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
npm install file-saver
npm install react-router-dom
```

### server

```
npm init -y
npm install cloudinary
npm install cors
npm install dotenv
npm install express
npm install mongoose
npm install mongodb
npm install nodemon
npm install openai
```

## 제작순서

1. 클라이언트 및 서버 기본 설정: React 및 Node.js 환경을 구축하고 필요한 라이브러리를 설치했습니다. 클라이언트는 Vite를 사용하여 개발 환경을 구성하고, Tailwind CSS로 스타일링을 적용했습니다. 서버는 Express와 MongoDB를 사용하여 REST API를 구축했습니다.
2. UI 컴포넌트 개발 및 라우팅 설정: React 컴포넌트를 개발하여 페이지 구조를 설계했습니다. react-router-dom을 사용하여 클라이언트 사이드 라우팅을 구현했습니다.
3. OpenAI DALL-E API 연동 및 데이터 처리: OpenAI의 DALL-E API를 통해 이미지 생성 기능을 통합했습니다. 서버에서 요청을 처리하고 결과를 클라이언트에 전달하는 방식으로 구현했습니다.

### 기술적 세부사항 요약

- React와 Vite: 모던 웹 애플리케이션 개발을 위해 React와 Vite를 사용하여 빠른 개발 환경과 성능을 보장합니다.
- Tailwind CSS: 유틸리티-퍼스트 CSS 프레임워크를 사용하여 반응형 디자인과 커스텀 스타일링을 적용합니다.
- OpenAI DALL-E API: 서버에서 OpenAI의 DALL-E API를 호출하여 사용자가 요청한 이미지를 생성하고, 결과를 클라이언트로 전송합니다.
- Express와 MongoDB: RESTful API 서버를 구축하여 데이터 관리 및 API 요청 처리를 담당합니다.

## 코드 미리보기

<details>
  <summary>😆 OpenAI DALL-E API를 이용한 이미지 생성 요청 처리</summary>

```javascript
app.post("/create-image", async (req, res) => {
  try {
    const response = await openai.createImage(req.body.prompt);
    res.send(response.data);
  } catch (error) {
    res.status(500).send(error);
  }
});
```

</details>

<details>
  <summary>😆 이미지 생성 요청에 대한 클라이언트 사이드 처리</summary>

```javascript
const createImage = async () => {
  try {
    const response = await axios.post("/create-image", { prompt: userPrompt });
    setImageUrl(response.data.imageUrl);
  } catch (error) {
    console.error("Error creating image:", error);
  }
};
```

</details>

<details>
  <summary>😆 이미지 및 로더 표시</summary>

```javascript
{form.photo ? (
  <img src={form.photo} alt={form.prompt} ... />
) : (
  <img src={preview} alt="preview" ... />
)}
{generatingImg && <div ... ><Loader /></div>}
```

</details>

생성된 이미지(form.photo)가 있으면 표시하고, 없으면 미리보기 이미지(preview)를 표시합니다.  
이미지 생성 중(generatingImg)일 때 로더 컴포넌트를 표시합니다.

<details>
  <summary>😆 Surprise Me 기능</summary>
  
```javascript
const handleSurpriseMe = () => {
  const randomPrompt = getRandomPrompt(form.prompt);
  setForm({ ...form, prompt: randomPrompt });
};
```
</details>

사용자에게 무작위 프롬프트를 제공하는 기능입니다.

<details>
  <summary>😆 입력 변경 핸들러</summary>

```javascript
const handleChange = (e) => {
  setForm({ ...form, [e.target.name]: e.target.value });
};
```

</details>

폼 필드의 값이 변경될 때마다 form 상태를 업데이트합니다.

<details>
  <summary>😆 검색 기능</summary>

```javascript
const handleSearchChange = (e) => {
  clearTimeout(searchTimeout);
  setSearchText(e.target.value);

  setSearchTimeout(
    setTimeout(() => {
      const searchResult = allPosts.filter(...);
      setSearchedResults(searchResult);
    }, 500)
  );
};
```

</details>

사용자가 검색 필드에 입력할 때마다 handleSearchChange 함수가 호출됩니다.  
입력값에 따라 게시물을 필터링하고, 결과를 searchedResults에 저장합니다.

## 트러블 슈팅

<details>
<summary>네트워크 지연 및 API 호출오류</summary>

```javascript
// 문제: 사용자 입력 검증이 없음
const handleSubmit = async (e) => {
  // API 호출 코드...
};
```

```javascript
// 개선: 사용자 입력 검증 추가
const handleSubmit = async (e) => {
  if (!form.name.trim() || !form.prompt.trim() || !form.photo) {
    alert("모든 필드를 채워주세요.");
    return;
  }
  // API 호출 코드...
};
```

<p>사용자가 모든 필드를 채우지 않았다면 경고 메시지를 표시하고, API 호출을 중단합니다. 이렇게 함으로써 사용자가 실수로 불완전한 데이터를 제출하는 것을 방지하고, 서버에 불필요한 요청을 보내는 것을 막습니다.</p>
</details>

<details>
<summary>네트워크 지연 및 API 실패</summary>

```javascript
// 문제: API 호출 실패에 대한 처리가 없음
const generateImage = async () => {
  // API 호출
  const data = await response.json();
  // 이미지 데이터 설정
};
```

```javascript
// 개선: try-catch 블록을 사용한 오류 처리
const generateImage = async () => {
  try {
    // API 호출
    if (!response.ok) {
      throw new Error("네트워크 오류 또는 서버 응답 오류");
    }
    // 데이터 유효성 검증
    if (!data.photo) {
      throw new Error("유효하지 않은 응답 데이터");
    }
    // 이미지 데이터 설정
  } catch (err) {
    alert("이미지 생성 중 오류가 발생했습니다: " + err.message);
  } finally {
    setGeneratingImg(false);
  }
};
```

<p>try-catch 블록을 사용하여 API 호출 과정에서 발생할 수 있는 오류를 처리합니다. 서버로부터의 응답이 성공적이지 않거나, 반환된 데이터가 유효하지 않을 경우 오류를 발생시키고, 피드백을 제공합니다.</p>
</details>

## 배포하기

서버 배포: Render 사용

- Render에 서버 배포: 서버 애플리케이션을 Render에 배포했습니다.
- API 주소 업데이트: 로컬 환경에서 개발한 후, 서버의 API 주소를 Render에서 제공하는 배포된 서버의 주소로 변경했습니다. 이를 통해 클라이언트 애플리케이션이 Render에 호스팅된 서버와 통신할 수 있도록 설정했습니다.

클라이언트 배포: Vercel 사용

- Vercel에 클라이언트 배포: 클라이언트 사이드 애플리케이션을 Vercel에 배포했습니다.

배포시 주의사항

- 보안 설정: 클라우드 서비스를 사용할 때는 보안 설정에 주의를 기울여야 합니다. API 키나 기타 중요한 정보는 환경 변수를 사용하여 관리하고, 외부에 노출되지 않도록 해야 합니다.
- CORS 설정: 클라이언트와 서버가 다른 도메인에 배포된 경우, CORS(Cross-Origin Resource Sharing) 문제가 발생할 수 있습니다. 서버 측에서 적절한 CORS 설정을 해주어야 클라이언트의 요청을 정상적으로 처리할 수 있습니다.
