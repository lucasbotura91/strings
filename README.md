<!DOCTYPE html>
<html lang="pt-BT">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Extrator de Palavras-Chave</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="container">
        <h1>Extrator de palavras-chave</h1>
        <textarea id="entrada-de-texto" placeholder="Digite ou cole seu texto aqui..."></textarea>
        <button id="botao-palavrachave">Extrair</button>
        <div id="resultado-palavrachave"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
const botaoMostraPalavras = document.querySelector('#botao-palavrachave');

botaoMostraPalavras.addEventListener('click', mostraPalavrasChave);

function mostraPalavrasChave() {
    const texto = document.querySelector('#entrada-de-texto').value;
    const campoResultado = document.querySelector('#resultado-palavrachave');
    const palavrasChave = processaTexto(texto);

    campoResultado.textContent = palavrasChave.join(", ");
}

function processaTexto(texto) {
    let palavras = texto.split(/\P{L}+/u);
    const frequencias = contaFrequencias(palavras);
    let ordenadas = Object.keys(frequencias).sort(ordenaPalavra);

    function ordenaPalavra(p1, p2) {
        return frequencias[p2] - frequencias[p1];
    }

    console.log(ordenadas);
    return ordenadas.slice(0, 10);
}

function contaFrequencias(palavras) {
    let frequencias = {};
    for (let i of palavras) {
        frequencias[i] = 0;
        for (let j of palavras) {
            if (i == j) {
                frequencias[i]++;
            }
        }
    }
    return frequencias;
}
