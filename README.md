<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <base target="_self">
    <title>FACE BURG - Delivery</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/@preline/preline@2.0.0/dist/preline.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: '#FF6B00',
                        secondary: '#FFD700',
                        dark: '#1A1A1A',
                    }
                }
            }
        }
    </script>
    <style>
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .cart-item-enter {
            animation: cartItemEnter 0.3s ease-out;
        }
        @keyframes cartItemEnter {
            from { transform: translateX(20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
    </style>
</head>
<body class="bg-gray-100 dark:bg-dark dark:text-white transition-colors duration-300">
    <div class="container mx-auto px-4 py-8 max-w-6xl">
        <!-- Header -->
        <header class="mb-8 text-center">
            <h1 class="text-4xl font-bold text-primary mb-2">FACE BURG</h1>
            <p class="text-gray-600 dark:text-gray-300 mb-4">Funcionamento: 18h às 1h | Segunda a Domingo</p>
            <div class="flex justify-center gap-4 mb-6">
                <button id="theme-toggle" class="p-2 rounded-full bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600 transition-colors">
                    <i class="fas fa-moon dark:hidden"></i>
                    <i class="fas fa-sun hidden dark:inline"></i>
                </button>
                <button id="cart-toggle" class="p-2 rounded-full bg-primary text-white hover:bg-orange-700 transition-colors relative">
                    <i class="fas fa-shopping-cart"></i>
                    <span id="cart-count" class="absolute -top-2 -right-2 bg-secondary text-dark rounded-full w-6 h-6 flex items-center justify-center text-sm font-bold">0</span>
                </button>
            </div>
        </header>

        <!-- Menu Sections -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <!-- Left Column - Hamburgers -->
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 fade-in">
                <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">HAMBÚRGUERES</h2>
                <div class="space-y-4" id="hamburgers">
                    <!-- Hamburgers will be inserted here by JS -->
                </div>
            </div>

            <!-- Middle Column - Fries, Açaí, Drinks -->
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 fade-in">
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">FRITAS</h2>
                    <div class="space-y-4" id="fries">
                        <!-- Fries will be inserted here by JS -->
                    </div>
                </div>
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">AÇAÍ (COPOS E TIGELAS)</h2>
                    <div class="space-y-4" id="acai">
                        <!-- Açaí items will be inserted here by JS -->
                    </div>
                </div>
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">REFRIGERANTES</h2>
                    <div class="space-y-4" id="drinks">
                        <!-- Drinks will be inserted here by JS -->
                    </div>
                </div>
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">CERVEJAS</h2>
                    <div class="space-y-4" id="beers">
                        <!-- Beers will be inserted here by JS -->
                    </div>
                </div>
                <div>
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">SUCOS</h2>
                    <div class="space-y-4" id="juices">
                        <!-- Juices will be inserted here by JS -->
                    </div>
                </div>
            </div>

            <!-- Right Column - Combos, Waters, Candies, Extras and Cart -->
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 fade-in">
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">COMBOS</h2>
                    <div class="space-y-4" id="combos">
                        <!-- Combos will be inserted here by JS -->
                    </div>
                </div>
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">ÁGUAS</h2>
                    <div class="space-y-4" id="waters">
                        <!-- Waters will be inserted here by JS -->
                    </div>
                </div>
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">BOMBONIERE</h2>
                    <div class="space-y-4" id="candies">
                        <!-- Candies will be inserted here by JS -->
                    </div>
                </div>
                <div class="mb-6">
                    <h2 class="text-2xl font-bold text-primary mb-4 border-b pb-2">ACRÉSCIMOS (ADICIONAIS)</h2>
                    <div class="space-y-4" id="extras">
                        <!-- Extras will be inserted here by JS -->
                    </div>
                </div>
                
                <!-- Cart -->
                <div id="cart-container" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex justify-end">
                    <div class="bg-white dark:bg-gray-800 w-full max-w-md h-full overflow-y-auto p-6 transform transition-transform duration-300">
                        <div class="flex justify-between items-center mb-4">
                            <h2 class="text-2xl font-bold text-primary">Seu Pedido</h2>
                            <button id="close-cart" class="text-gray-500 hover:text-gray-700 dark:hover:text-gray-300">
                                <i class="fas fa-times text-xl"></i>
                            </button>
                        </div>
                        
                        <div id="cart-items" class="mb-4 space-y-3">
                            <!-- Cart items will be inserted here by JS -->
                        </div>
                        
                        <div class="border-t pt-4 mb-4">
                            <div class="flex justify-between font-bold text-lg">
                                <span>Total:</span>
                                <span id="cart-total">R$ 0,00</span>
                            </div>
                        </div>
                        
                        <div class="space-y-4">
                            <div>
                                <label for="customer-name" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Nome Completo</label>
                                <input type="text" id="customer-name" class="w-full px-3 py-2 border rounded-md dark:bg-gray-700 dark:border-gray-600">
                            </div>
                            <div>
                                <label for="customer-address" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">Endereço Completo</label>
                                <input type="text" id="customer-address" class="w-full px-3 py-2 border rounded-md dark:bg-gray-700 dark:border-gray-600">
                            </div>
                            
                            <button id="send-order" class="w-full py-3 px-4 bg-gray-300 text-gray-700 font-bold rounded-md cursor-not-allowed" disabled>
                                ENVIAR PEDIDO
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Menu data
        const menuItems = {
            hamburgers: [
                { name: "SUPREMO", price: 31.00 },
                { name: "F-PICANHA", price: 35.00 },
                { name: "F-PICANHA DUPLO", price: 45.00 },
                { name: "F-ANGUS", price: 35.00 },
                { name: "F-ANGUS DUPLO", price: 45.00 },
                { name: "F-AMERICANO", price: 31.00 },
                { name: "F-AUSTRALIANO", price: 29.00 },
                { name: "F-SALADA", price: 17.00 },
                { name: "F-BACON", price: 26.00 },
                { name: "F-BURGUER", price: 16.00 },
                { name: "F-CALABRESA", price: 25.00 },
                { name: "F-EGG", price: 19.00 },
                { name: "F-EGG BACON", price: 27.00 },
                { name: "F-FILÉ", price: 31.00 },
                { name: "F-FRANGO", price: 25.00 },
                { name: "F-LOMBO", price: 24.00 },
                { name: "F-TUDO", price: 33.00 },
                { name: "FACEBURG", price: 29.00 },
                { name: "FRANBACON", price: 29.00 },
                { name: "MISTO QUENTE", price: 8.00 },
                { name: "VEGETARIANO", price: 27.00 }
            ],
            fries: [
                { name: "FRITAS", price: 10.00 }
            ],
            acai: [
                { name: "FACE OREO", price: 24.00 },
                { name: "COPO DE AÇAÍ MONTADO 500ML (Face Bis, Delícia, Brasil, Kids, Ninho, Ouro, Tropical)", price: 21.00 },
                { name: "COPO DE AÇAÍ MONTADO 500ML (Face dos Sonhos)", price: 22.00 },
                { name: "COPO DE AÇAÍ MONTADO 500ML (Face Especial)", price: 23.00 },
                { name: "COPO DE AÇAÍ MONTADO 500ML (Face Nutella)", price: 24.00 },
                { name: "TIGELA DE AÇAÍ CASADINHO 1L", price: 37.00 },
                { name: "TIGELA DE AÇAÍ TRADICIONAL 1L", price: 37.00 },
                { name: "TIGELA DE AÇAÍ CASADINHO 300ML", price: 18.00 },
                { name: "TIGELA DE AÇAÍ TRADICIONAL 300ML", price: 18.00 },
                { name: "TIGELA DE AÇAÍ CASADINHO 500ML", price: 21.00 },
                { name: "TIGELA DE AÇAÍ TRADICIONAL 500ML", price: 21.00 }
            ],
            combos: [
                { name: "FACE COMBO 1 AMERI", price: 26.00 },
                { name: "FACE COMBO 2 AUSTRA", price: 25.00 },
                { name: "FACE COMBO 4 BACON", price: 23.50 },
                { name: "COMBO F-CALABRESA", price: 27.50 },
                { name: "COMBO F-BACON", price: 27.50 },
                { name: "COMBO F-PICANHA C/ FRITAS", price: 34.99 },
                { name: "F-BACON + FRITAS + REFRI LATA", price: 30.00 }
            ],
            drinks: [
                { name: "REFRIGERANTE 2L (Coca-Cola, Fanta Uva, Fanta Laranja, Sprite, Guaraná)", price: 16.00 },
                { name: "PEPSI 1L", price: 10.00 },
                { name: "REFRIGERANTE 1L (Coca-Cola)", price: 12.00 },
                { name: "REFRIGERANTE 1L (Guaraná Antártica)", price: 11.00 },
                { name: "REFRIGERANTE 600ML (Sprite, Fanta Laranja, Coca-Cola, Fanta Uva, Guaraná Antártica)", price: 9.00 },
                { name: "H2O", price: 9.00 },
                { name: "GUARANÁ MINEIRO 350ML", price: 5.00 },
                { name: "REFRIGERANTE LATA (Coca-Cola, Fanta Laranja, Fanta Uva, Guaraná Antártica, Sprite)", price: 7.00 },
                { name: "COCA-COLA ZERO 350ML", price: 7.00 },
                { name: "RED BULL", price: 15.00 }
            ],
            beers: [
                { name: "HEINEKEN 330ML", price: 11.00 },
                { name: "BUDWEISER LONG", price: 10.00 },
                { name: "SPATEN LONG", price: 9.00 },
                { name: "BRAHMA 355ML LONG", price: 9.00 }
            ],
            juices: [
                { name: "SUCO LARANJA", price: 8.00 },
                { name: "SUCO ACEROLA NATURAL", price: 10.00 },
                { name: "SUCO ABACAXI C/ HORTELÃ", price: 10.00 },
                { name: "SUCO GOIABA NATURAL", price: 10.00 },
                { name: "SUCO MARACUJÁ NATURAL", price: 12.00 },
                { name: "SUCO DEL VALLE UVA", price: 6.00 },
                { name: "SUCO DEL VALLE PÊSSEGO", price: 6.00 },
                { name: "SUCO DEL VALLE MARACUJÁ LATA", price: 6.00 }
            ],
            waters: [
                { name: "ÁGUA SEM GÁS", price: 5.00 },
                { name: "ÁGUA COM GÁS", price: 5.00 }
            ],
            candies: [
                { name: "BALAS", price: 0.10 },
                { name: "BOMBOM", price: 1.00 },
                { name: "BATON", price: 2.00 },
                { name: "CARIBE", price: 3.00 },
                { name: "CHICLETS", price: 0.25 },
                { name: "CHOKITO", price: 2.50 },
                { name: "HALLS", price: 2.00 },
                { name: "MENTOS", price: 2.00 },
                { name: "PRESTÍGIO", price: 2.50 },
                { name: "TALENTO 56G", price: 2.50 },
                { name: "TRENTO", price: 3.00 },
                { name: "TRIDENT", price: 2.00 },
                { name: "DIAMANTE NEGRO", price: 2.00 },
                { name: "LAKA 34G", price: 2.00 },
                { name: "KITKAT", price: 5.00 },
                { name: "TALENTO GRANDE", price: 5.50 }
            ],
            extras: [
                { name: "MOLHO ESPECIAL", price: 2.00 },
                { name: "ABACAXI ADICIONAL", price: 1.50 },
                { name: "BACON ADICIONAL", price: 5.00 },
                { name: "BIFE ARTESANAL", price: 0.00 },
                { name: "HAMBÚRGUER 56G ADICIONAL", price: 2.50 },
                { name: "HAMBÚRGUER ARTESANAL 180G", price: 6.50 },
                { name: "HAMBÚRGUER DE PICANHA 90G ADICIONAL", price: 4.50 },
                { name: "CALABRESA ADICIONAL", price: 5.00 },
                { name: "CREME CHEDDAR ADICIONAL", price: 5.00 },
                { name: "FILÉ ADICIONAL", price: 8.00 },
                { name: "LOMBO ADICIONAL", price: 5.00 },
                { name: "FRANGO ADICIONAL", price: 6.00 },
                { name: "OVO ADICIONAL", price: 2.00 },
                { name: "PRESUNTO ADICIONAL", price: 2.50 },
                { name: "QUEIJO MUSSARELA ADICIONAL", price: 2.00 },
                { name: "SALSICHA ADICIONAL", price: 2.00 }
            ]
        };

        // Cart state
        let cart = [];
        
        // DOM elements
        const cartCountEl = document.getElementById('cart-count');
        const cartItemsEl = document.getElementById('cart-items');
        const cartTotalEl = document.getElementById('cart-total');
        const cartContainerEl = document.getElementById('cart-container');
        const cartToggleEl = document.getElementById('cart-toggle');
        const closeCartEl = document.getElementById('close-cart');
        const sendOrderBtn = document.getElementById('send-order');
        const customerNameEl = document.getElementById('customer-name');
        const customerAddressEl = document.getElementById('customer-address');
        const themeToggleEl = document.getElementById('theme-toggle');

        // Initialize menu
        function initMenu() {
            Object.keys(menuItems).forEach(section => {
                const container = document.getElementById(section);
                if (container) {
                    menuItems[section].forEach(item => {
                        const itemEl = document.createElement('div');
                        itemEl.className = 'flex justify-between items-center p-3 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-md transition-colors';
                        itemEl.innerHTML = `
                            <div class="flex-1">
                                <h3 class="font-medium">${item.name}</h3>
                            </div>
                            <div class="flex items-center gap-3">
                                <span class="font-bold text-primary">R$ ${item.price.toFixed(2).replace('.', ',')}</span>
                                <button class="add-to-cart bg-primary text-white p-2 rounded-full hover:bg-orange-700 transition-colors" data-name="${item.name}" data-price="${item.price}">
                                    <i class="fas fa-plus"></i>
                                </button>
                            </div>
                        `;
                        container.appendChild(itemEl);
                    });
                }
            });
        }

        // Add to cart
        function addToCart(name, price) {
            const existingItem = cart.find(item => item.name === name);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({ name, price, quantity: 1 });
            }
            
            updateCart();
            showCart();
        }

        // Remove from cart
        function removeFromCart(name) {
            const itemIndex = cart.findIndex(item => item.name === name);
            
            if (itemIndex !== -1) {
                if (cart[itemIndex].quantity > 1) {
                    cart[itemIndex].quantity -= 1;
                } else {
                    cart.splice(itemIndex, 1);
                }
                
                updateCart();
            }
        }

        // Update cart UI
        function updateCart() {
            // Update count
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCountEl.textContent = totalItems;
            
            // Update items list
            cartItemsEl.innerHTML = '';
            
            if (cart.length === 0) {
                cartItemsEl.innerHTML = '<p class="text-gray-500 dark:text-gray-400">Seu carrinho está vazio</p>';
                sendOrderBtn.disabled = true;
                sendOrderBtn.className = 'w-full py-3 px-4 bg-gray-300 text-gray-700 font-bold rounded-md cursor-not-allowed';
            } else {
                cart.forEach(item => {
                    const itemEl = document.createElement('div');
                    itemEl.className = 'flex justify-between items-center p-3 bg-gray-100 dark:bg-gray-700 rounded-md cart-item-enter';
                    itemEl.innerHTML = `
                        <div class="flex-1">
                            <h3 class="font-medium">${item.name}</h3>
                            <p class="text-sm text-gray-600 dark:text-gray-300">R$ ${item.price.toFixed(2).replace('.', ',')} x ${item.quantity}</p>
                        </div>
                        <div class="flex items-center gap-2">
                            <span class="font-bold">R$ ${(item.price * item.quantity).toFixed(2).replace('.', ',')}</span>
                            <div class="flex items-center gap-1">
                                <button class="remove-item text-red-500 hover:text-red-700 dark:hover:text-red-400 p-1" data-name="${item.name}">
                                    <i class="fas fa-minus"></i>
                                </button>
                                <button class="add-item text-green-500 hover:text-green-700 dark:hover:text-green-400 p-1" data-name="${item.name}">
                                    <i class="fas fa-plus"></i>
                                </button>
                            </div>
                        </div>
                    `;
                    cartItemsEl.appendChild(itemEl);
                });
                
                // Update total
                const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
                cartTotalEl.textContent = `R$ ${total.toFixed(2).replace('.', ',')}`;
                
                // Check if order can be sent
                checkOrderReady();
            }
        }

        // Show/hide cart
        function showCart() {
            cartContainerEl.classList.remove('hidden');
        }

        function hideCart() {
            cartContainerEl.classList.add('hidden');
        }

        // Check if order is ready to be sent
        function checkOrderReady() {
            const name = customerNameEl.value.trim();
            const address = customerAddressEl.value.trim();
            
            if (name && address && cart.length > 0) {
                sendOrderBtn.disabled = false;
                sendOrderBtn.className = 'w-full py-3 px-4 bg-green-500 text-white font-bold rounded-md hover:bg-green-600 transition-colors';
            } else {
                sendOrderBtn.disabled = true;
                sendOrderBtn.className = 'w-full py-3 px-4 bg-gray-300 text-gray-700 font-bold rounded-md cursor-not-allowed';
            }
        }

        // Format order message for WhatsApp
        function formatOrderMessage() {
            const name = customerNameEl.value.trim();
            const address = customerAddressEl.value.trim();
            
            let message = `Olá, este é o meu pedido de hoje!\n\n`;
            message += `*PEDIDO FACE BURG*\n\n`;
            message += `*Cliente:* ${name}\n`;
            message += `*Endereço:* ${address}\n\n`;
            message += `*Itens:*\n`;
            
            cart.forEach(item => {
                message += `- ${item.name} (${item.quantity}x) - R$ ${(item.price * item.quantity).toFixed(2).replace('.', ',')}\n`;
            });
            
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            message += `\n*Total: R$ ${total.toFixed(2).replace('.', ',')}*`;
            
            return encodeURIComponent(message);
        }

        // Event listeners
        document.addEventListener('DOMContentLoaded', () => {
            initMenu();
            
            // Add to cart buttons
            document.addEventListener('click', (e) => {
                if (e.target.classList.contains('add-to-cart') || e.target.closest('.add-to-cart')) {
                    const button = e.target.classList.contains('add-to-cart') ? e.target : e.target.closest('.add-to-cart');
                    const name = button.dataset.name;
                    const price = parseFloat(button.dataset.price);
                    addToCart(name, price);
                }
                
                // Remove item buttons in cart
                if (e.target.classList.contains('remove-item') || e.target.closest('.remove-item')) {
                    const button = e.target.classList.contains('remove-item') ? e.target : e.target.closest('.remove-item');
                    const name = button.dataset.name;
                    removeFromCart(name);
                }
                
                // Add item buttons in cart
                if (e.target.classList.contains('add-item') || e.target.closest('.add-item')) {
                    const button = e.target.classList.contains('add-item') ? e.target : e.target.closest('.add-item');
                    const name = button.dataset.name;
                    const item = cart.find(item => item.name === name);
                    if (item) addToCart(name, item.price);
                }
            });
            
            // Cart toggle
            cartToggleEl.addEventListener('click', showCart);
            closeCartEl.addEventListener('click', hideCart);
            
            // Check if order can be sent when inputs change
            customerNameEl.addEventListener('input', checkOrderReady);
            customerAddressEl.addEventListener('input', checkOrderReady);
            
            // Send order
            sendOrderBtn.addEventListener('click', (e) => {
                e.preventDefault();
                const message = formatOrderMessage();
                window.open(`https://wa.me/5538998722422?text=${message}`, '_blank');
            });
            
            // Theme toggle
            themeToggleEl.addEventListener('click', () => {
                document.documentElement.classList.toggle('dark');
                localStorage.setItem('theme', document.documentElement.classList.contains('dark') ? 'dark' : 'light');
            });
            
            // Check for saved theme preference
            if (localStorage.getItem('theme') === 'dark' || (!localStorage.getItem('theme') && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        });
    </script>
</body>
</html>
