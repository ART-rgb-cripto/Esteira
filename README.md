let productPosition = 10; // Posição inicial do produto
const compartments = [
  { id: "compartment1", basketId: "basket1", right: 200 },
  { id: "compartment2", basketId: "basket2", right: 50 },
];

// Movimento contínuo do produto na esteira
function moveProduct() {
  const product = document.getElementById("product");
  productPosition += 10;
  product.style.left = ${productPosition}px;

  // Verificar cada comporta
  compartments.forEach((compartment) => {
    checkCompartment(compartment);
  });

  // Reiniciar a posição do produto se ele ultrapassar a esteira
  if (productPosition > 800) {
    productPosition = 10;
  }

  // Continuar movimento
  setTimeout(moveProduct, 200);
}

// Verificar comporta automaticamente
function checkCompartment(compartment) {
  const product = document.getElementById("product");
  const productRect = product.getBoundingClientRect();
  const compartmentElement = document.getElementById(compartment.id);
  const basketElement = document.getElementById(compartment.basketId);
  const compartmentRect = compartmentElement.getBoundingClientRect();

  // Verificar se o produto está alinhado com a comporta
  if (Math.abs(productRect.left - (800 - compartment.right)) < 50) {
    const basketState = compartmentElement.getAttribute("data-basket-state");

    if (basketState === "empty") {
      // Abrir comporta e encher a cesta
      compartmentElement.classList.add("open");
      basketElement.classList.add("full");
      compartmentElement.setAttribute("data-basket-state", "full");

      // Fechar comporta após 1 segundo
      setTimeout(() => {
        compartmentElement.classList.remove("open");
      }, 1000);
    } else if (basketState === "full") {
      console.log(A cesta da comporta ${compartment.id} está cheia!);
    } else {
      console.log(Sem cesta na comporta ${compartment.id}!);
    }
  }
}

// Iniciar o movimento automático
moveProduct();
