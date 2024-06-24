Мэдээж, локал веб серверийг эхлүүлэхдээ Node.js ашиглах зааврыг оруулж өгье. Доорх нь Node.js ашиглан локал веб серверийг хэрхэн эхлүүлэх талаар тайлбарласан хувилбар юм:

# WebAssembly Example

Энэ төсөл нь WebAssembly (WASM) ашиглан факториал функцыг веб дээр хэрхэн гүйцэтгэхийг харуулж байна.

## Шаардлагатай хэрэгслүүд

- [Emscripten](https://emscripten.org/) компилятор
- Орчин үеийн веб хөтөч (Chrome, Firefox, Safari, Edge)
- [Node.js](https://nodejs.org/)

## Emscripten-ийг суулгах

Энэ заавар нь `emcc` (Emscripten компилятор) хэрэгслийг хэрхэн суулгах талаар тайлбарлана.

1. `emsdk` репозиторийг клонийгоор татаж авна:
    ```bash
    git clone https://github.com/emscripten-core/emsdk.git
    ```

2. `emsdk` директори руу орно:
    ```bash
    cd emsdk
    ```

3. Бүх хэрэгслүүдийг татаж суулгана:
    ```bash
    ./emsdk install latest
    ```

4. Бүх хэрэгслүүдийг идэвхжүүлнэ:
    ```bash
    ./emsdk activate latest
    ```

5. `emsdk_env.sh` скриптийг эхлүүлж Emscripten орчны замуудыг тохируулна:
    ```bash
    source ./emsdk_env.sh
    ```

## C хэлний кодыг WebAssembly руу хөрвүүлэх

Энгийн C хэлний кодыг WebAssembly (WASM) руу хөрвүүлэхийн тулд дараах командыг ажиллуулна:
```bash
emcc factorial.c -s WASM=1 -s EXPORTED_FUNCTIONS="['_factorial']" -o factorial.js
```

## Локал веб серверийг эхлүүлэх (Node.js ашиглан)

1. Node.js суулгасан эсэхээ шалгана. Хэрэв суулгаагүй бол [эндээс](https://nodejs.org/) татаж суулгана уу.
2. `serve` модулийг глобал байдлаар суулгана:
    ```bash
    npm install -g serve
    ```

3. Веб серверийг эхлүүлнэ:
    ```bash
    serve
    ```

4. Веб хөтөч дээрээ `http://localhost:3000` хаягаар орж, төслийнхөө үр дүнг шалгана.
