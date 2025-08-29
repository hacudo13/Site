<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Save More - Oferta Shopee</title>
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- EDITE AQUI -->
  <script>
    // coloque o preço atual aqui, por exemplo: 'R$ 12,90'
    const PRODUCT_PRICE = 'R$86,99';
    const AFF_LINK = 'https://s.shopee.com.br/4Aq9Vl56ei';
    const PRODUCT_IMG = 'https://down-br.img.susercontent.com/file/br-11134207-7r98o-ltp1m27uh9kq52';
    const PRODUCT_TITLE = 'Produto Exclusivo Save More';
  </script>
</head>
<body class="bg-gray-50 font-sans leading-relaxed">

  <!-- Hero -->
  <section class="bg-orange-500 text-white text-center py-12 px-4">
    <h1 class="text-3xl font-bold mb-4">🔥 Save More apresenta: Oferta Exclusiva!</h1>
    <p class="text-lg">Aproveite preço especial — promoção por tempo limitado.</p>
  </section>

  <!-- Produto -->
  <section class="max-w-4xl mx-auto p-6">
    <div class="bg-white rounded-2xl shadow-lg p-6">
      <img id="productImg" src="" alt="Produto Shopee" class="w-full rounded-xl mb-6">

      <h2 id="productTitle" class="text-2xl font-bold mb-2 text-gray-800"></h2>
      <p class="text-gray-600 mb-4">
        Descubra porque tantas pessoas estão comprando este produto na Shopee.
      </p>

      <!-- Valor (preenchido por JS) -->
      <p id="86,99" class="text-3xl font-extrabold text-orange-600 mb-6"></p>

      <ul class="list-disc pl-6 text-gray-700 mb-6">
        <li>✅ Qualidade garantida</li>
        <li>✅ Ótimo custo-benefício</li>
        <li>✅ Entrega rápida pela Shopee</li>
      </ul>

      <div class="text-center">
        <a id="buyBtn" href="#" target="_blank"
           class="bg-orange-500 text-white px-6 py-3 rounded-xl font-bold shadow-lg hover:bg-orange-600 transition inline-flex items-center gap-2">
          👉 Comprar na Shopee <span id="buyPrice" class="ml-2 font-bold"></span>
        </a>
      </div>
    </div>
  </section>

  <!-- Depoimentos -->
  <section class="max-w-4xl mx-auto p-6">
    <h2 class="text-2xl font-bold text-center mb-6">O que nossos clientes dizem</h2>
    <div class="grid md:grid-cols-3 gap-6">
      <div class="bg-white shadow-md rounded-xl p-4">
        <p class="text-gray-600 italic">"Chegou rápido e tudo certo!"</p>
        <span class="block mt-2 font-bold text-gray-800">— Maria S.</span>
      </div>
      <div class="bg-white shadow-md rounded-xl p-4">
        <p class="text-gray-600 italic">"Recomendo, excelente custo-benefício."</p>
        <span class="block mt-2 font-bold text-gray-800">— João P.</span>
      </div>
      <div class="bg-white shadow-md rounded-xl p-4">
        <p class="text-gray-600 italic">"Ótimo preço e entrega antes do prazo."</p>
        <span class="block mt-2 font-bold text-gray-800">— Viviane R.</span>
      </div>
    </div>
  </section>

  <!-- CTA Final -->
  <section class="bg-orange-500 text-white text-center py-10">
    <h2 class="text-2xl font-bold mb-4">Garanta o seu agora mesmo com a Save More!</h2>
    <a id="buyBtnFooter" href="#" target="_blank"
       class="bg-white text-orange-600 px-8 py-4 rounded-xl font-bold shadow-lg hover:bg-gray-200 transition inline-flex items-center gap-2">
      Comprar na Shopee <span id="buyPriceFooter" class="font-bold"></span>
    </a>
  </section>

  <footer class="text-center text-gray-500 py-6 text-sm">
    © 2025 - Save More Afiliados | Não é o site oficial da Shopee.
  </footer>

  <script>
    // Não precisa mexer aqui se editou a constante PRODUCT_PRICE acima
    document.getElementById('productImg').src = PRODUCT_IMG;
    document.getElementById('productTitle').innerText = PRODUCT_TITLE;

    const showPrice = (p) => {
      if (!p || p === 'R$ X,XX') {
        document.getElementById('price').innerText = 'Confira o preço na Shopee';
        document.getElementById('buyPrice').innerText = '';
        document.getElementById('buyPriceFooter').innerText = '';
      } else {
        document.getElementById('price').innerText = `Apenas ${p} 🔥`;
        document.getElementById('buyPrice').innerText = p;
        document.getElementById('buyPriceFooter').innerText = p;
      }
      document.getElementById('buyBtn').href = AFF_LINK;
      document.getElementById('buyBtnFooter').href = AFF_LINK;
    };

    showPrice(PRODUCT_PRICE);
  </script>

</body>
</html>
