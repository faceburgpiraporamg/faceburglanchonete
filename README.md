<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FACE BURG - Delivery</title>
    <base target="_self">
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
                        secondary: '#FF9500',
                        dark: '#1E1E1E',
                        light: '#F5F5F5'
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
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .cart-item:hover {
            transform: translateX(5px);
            transition: transform 0.2s ease;
        }
        .send-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        .menu-category {
            scroll-margin-top: 1rem;
        }
    </style>
</head>
<body class="bg-gray-50 dark:bg-dark text-gray-800 dark:text-gray-200 min-h-screen">
    <div class="container mx-auto px-4 py-8">
        <header class="flex justify-between items-center mb-8">
            <div class="flex items-center">
                <img src="https://via.placeholder.com/50" alt="FACE BURG Logo" class="h-12 mr-3">
                <h1 class="text-2xl font-bold text-primary">FACE BURG</h1>
            </div>
            <div class="flex items-center space-x-4">
                <button id="theme-toggle" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700">
                    <i class="fas fa-moon dark:hidden"></i>
                    <i class="fas fa-sun hidden dark:inline"></i>
                </button>
                <div class="relative">
                    <button id="cart-btn" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700 relative">
                        <i class="fas fa-shopping-cart text-xl"></i>
                        <span id="cart-count" class="absolute -top-1 -right-1 bg-primary text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">0</span>
                    </button>
                </div>
            </div>
        </header>

        <div class="text-center mb-8">
            <p class="text-sm text-gray-600 dark:text-gray-400">
                <i class="fas fa-clock mr-1"></i> Funcionamento: 18h às 1h | Segunda a Domingo
            </p>
        </div>

        <div class="flex overflow-x-auto mb-6 pb-2 space-x-2">
            <a href="#hamburgers" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Hambúrgueres</a>
            <a href="#fries" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Fritas</a>
            <a href="#acai" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Açaí</a>
            <a href="#combos" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Combos</a>
            <a href="#drinks" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Refrigerantes</a>
            <a href="#sodas" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Refri Lata</a>
            <a href="#beers" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Cervejas</a>
            <a href="#juices" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Sucos</a>
            <a href="#waters" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Águas</a>
            <a href="#candies" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Bomboniere</a>
            <a href="#extras" class="category-link px-4 py-2 bg-white dark:bg-gray-800 rounded-full shadow-sm whitespace-nowrap">Adicionais</a>
        </div>

        <main class="grid lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2">
                <!-- Menu sections will be generated here by JavaScript -->
            </div>

            <div class="hidden lg:block">
                <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 sticky top-4">
                    <h2 class="text-xl font-bold mb-4 text-primary">Seu Carrinho</h2>
                    <div id="cart-items" class="mb-4 max-h-96 overflow-y-auto">
                        <p class="text-gray-500 dark:text-gray-400 text-center py-4">Seu carrinho está vazio</p>
                    </div>
                    <div class="border-t border-gray-200 dark:border-gray-700 pt-4">
                        <div class="flex justify-between mb-2">
                            <span>Subtotal:</span>
                            <span id="subtotal">R$ 0,00</span>
                        </div>
                        <div class="mb-4">
                            <label for="customer-name" class="block text-sm font-medium mb-1">Nome Completo*</label>
                            <input type="text" id="customer-name" class="w-full px-3 py-2 border rounded-md dark:bg-gray-700 dark:border-gray-600" required>
                        </div>
                        <div class="mb-4">
                            <label for="customer-address" class="block text-sm font-medium mb-1">Endereço Completo*</label>
                            <textarea id="customer-address" rows="3" class="w-full px-3 py-2 border rounded-md dark:bg-gray-700 dark:border-gray-600" required></textarea>
                        </div>
                        <button id="send-order" disabled class="send-btn w-full bg-gray-300 text-gray-600 py-3 rounded-md font-medium transition-colors">
                            ENVIAR PEDIDO
                        </button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- Mobile Cart Sidebar -->
    <div id="mobile-cart" class="fixed inset-0 bg-black bg-opacity-50 z-50 hidden">
        <div class="absolute right-0 top-0 h-full w-full max-w-md bg-white dark:bg-gray-800 shadow-lg transform transition-transform duration-300 translate-x-full">
            <div class="p-4 flex justify-between items-center border-b dark:border-gray-700">
                <h2 class="text-xl font-bold text-primary">Seu Carrinho</h2>
                <button id="close-cart" class="p-2">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div id="mobile-cart-items" class="p-4 max-h-[60vh] overflow-y-auto">
                <p class="text-gray-500 dark:text-gray-400 text-center py-4">Seu carrinho está vazio</p>
            </div>
            <div class="p-4 border-t dark:border-gray-700">
                <div class="flex justify-between mb-2">
                    <span>Subtotal:</span>
                    <span id="mobile-subtotal">R$ 0,00</span>
                </div>
                <div class="mb-4">
                    <label for="mobile-customer-name" class="block text-sm font-medium mb-1">Nome Completo*</label>
                    <input type="text" id="mobile-customer-name" class="w-full px-3 py-2 border rounded-md dark:bg-gray-700 dark:border-gray-600" required>
                </div>
                <div class="mb-4">
                    <label for="mobile-customer-address" class="block text-sm font-medium mb-1">Endereço Completo*</label>
                    <textarea id="mobile-customer-address" rows="3" class="w-full px-3 py-2 border rounded-md dark:bg-gray-700 dark:border-gray-600" required></textarea>
                </div>
                <button id="mobile-send-order" disabled class="send-btn w-full bg-gray-300 text-gray-600 py-3 rounded-md font-medium transition-colors">
                    ENVIAR PEDIDO
                </button>
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
                { name: "COCA-COLA ZERO 350ML", price: 7.00 },
                { name: "RED BULL", price: 15.00 }
            ],
            sodas: [
                { name: "REFRIGERANTE LATA (Coca-Cola)", price: 7.00 },
                { name: "REFRIGERANTE LATA (Fanta Laranja)", price: 7.00 },
                { name: "REFRIGERANTE LATA (Fanta Uva)", price: 7.00 },
                { name: "REFRIGERANTE LATA (Guaraná Antártica)", price: 7.00 },
                { name: "REFRIGERANTE LATA (Sprite)", price: 7.00 }
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

        // Cart data
        let cart = [];
        
        // DOM elements
        const cartItemsEl = document.getElementById('cart-items');
        const mobileCartItemsEl = document.getElementById('mobile-cart-items');
        const cartCountEl = document.getElementById('cart-count');
        const subtotalEl = document.getElementById('subtotal');
        const mobileSubtotalEl = document.getElementById('mobile-subtotal');
        const sendOrderBtn = document.getElementById('send-order');
        const mobileSendOrderBtn = document.getElementById('mobile-send-order');
        const customerNameEl = document.getElementById('customer-name');
        const customerAddressEl = document.getElementById('customer-address');
        const mobileCustomerNameEl = document.getElementById('mobile-customer-name');
        const mobileCustomerAddressEl = document.getElementById('mobile-customer-address');
        const cartBtn = document.getElementById('cart-btn');
        const mobileCart = document.getElementById('mobile-cart');
        const closeCartBtn = document.getElementById('close-cart');
        const themeToggleBtn = document.getElementById('theme-toggle');
        const categoryLinks = document.querySelectorAll('.category-link');

        // Initialize the app
        document.addEventListener('DOMContentLoaded', () => {
            renderMenu();
            setupEventListeners();
            checkThemePreference();
        });

        // Render the menu
        function renderMenu() {
            const menuContainer = document.querySelector('main > div.lg\\:col-span-2');
            
            // Clear existing menu
            menuContainer.innerHTML = '';
            
            // Render each category
            renderCategory('hamburgers', 'Hambúrgueres', 'hamburgers');
            renderCategory('fries', 'Fritas', 'fries');
            renderCategory('acai', 'Açaí (Copos e Tigelas)', 'acai');
            renderCategory('combos', 'Combos', 'combos');
            renderCategory('drinks', 'Refrigerantes', 'drinks');
            renderCategory('sodas', 'Refrigerantes em Lata', 'sodas');
            renderCategory('beers', 'Cervejas', 'beers');
            renderCategory('juices', 'Sucos', 'juices');
            renderCategory('waters', 'Águas', 'waters');
            renderCategory('candies', 'Bomboniere', 'candies');
            renderCategory('extras', 'Acréscimos (Adicionais)', 'extras');
        }

        function renderCategory(categoryId, categoryName, anchorId) {
            const menuContainer = document.querySelector('main > div.lg\\:col-span-2');
            
            const section = document.createElement('div');
            section.className = 'mb-12 fade-in menu-category';
            section.id = anchorId;
            section.innerHTML = `
                <h3 class="text-xl font-semibold mb-4 text-primary">${categoryName}</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4" id="menu-section-${categoryId}"></div>
            `;
            menuContainer.appendChild(section);
            
            menuItems[categoryId].forEach(item => {
                createMenuItem(item, categoryId);
            });
        }

        function createMenuItem(item, categoryId) {
            const container = document.getElementById(`menu-section-${categoryId}`);
            
            const itemEl = document.createElement('div');
            itemEl.className = 'bg-white dark:bg-gray-800 rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow';
            itemEl.innerHTML = `
                <div class="p-4">
                    <div class="flex justify-between items-start">
                        <h4 class="font-medium">${item.name}</h4>
                        <span class="font-semibold text-primary">R$ ${item.price.toFixed(2).replace('.', ',')}</span>
                    </div>
                    <button class="add-to-cart mt-3 w-full py-2 bg-primary hover:bg-secondary text-white rounded-md transition-colors" 
                            data-name="${item.name}" data-price="${item.price}">
                        Adicionar
                    </button>
                </div>
            `;
            container.appendChild(itemEl);
        }

        // Event listeners
        function setupEventListeners() {
            // Add to cart buttons
            document.addEventListener('click', (e) => {
                if (e.target.classList.contains('add-to-cart')) {
                    const name = e.target.dataset.name;
                    const price = parseFloat(e.target.dataset.price);
                    addToCart(name, price);
                }
            });

            // Cart buttons
            cartBtn.addEventListener('click', () => {
                mobileCart.classList.remove('hidden');
                document.querySelector('#mobile-cart > div').classList.remove('translate-x-full');
            });

            closeCartBtn.addEventListener('click', () => {
                document.querySelector('#mobile-cart > div').classList.add('translate-x-full');
                setTimeout(() => {
                    mobileCart.classList.add('hidden');
                }, 300);
            });

            // Form validation
            [customerNameEl, customerAddressEl, mobileCustomerNameEl, mobileCustomerAddressEl].forEach(el => {
                el.addEventListener('input', validateForm);
            });

            // Send order buttons
            sendOrderBtn.addEventListener('click', sendOrder);
            mobileSendOrderBtn.addEventListener('click', sendOrder);

            // Theme toggle
            themeToggleBtn.addEventListener('click', toggleTheme);

            // Category links
            categoryLinks.forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    const targetId = link.getAttribute('href').substring(1);
                    const targetElement = document.getElementById(targetId);
                    if (targetElement) {
                        targetElement.scrollIntoView({ behavior: 'smooth' });
                    }
                });
            });
        }

        // Cart functions
        function addToCart(name, price) {
            const existingItem = cart.find(item => item.name === name);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    name,
                    price,
                    quantity: 1
                });
            }
            
            updateCart();
            
            // Show feedback
            const feedback = document.createElement('div');
            feedback.className = 'fixed bottom-4 right-4 bg-primary text-white px-4 py-2 rounded-md shadow-lg animate-bounce';
            feedback.textContent = `${name} adicionado ao carrinho!`;
            document.body.appendChild(feedback);
            
            setTimeout(() => {
                feedback.remove();
            }, 2000);
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCart();
        }

        function updateCart() {
            // Update cart count
            const count = cart.reduce((total, item) => total + item.quantity, 0);
            cartCountEl.textContent = count;
            
            // Update cart items
            renderCartItems();
            
            // Update subtotal
            const subtotal = cart.reduce((total, item) => total + (item.price * item.quantity), 0);
            subtotalEl.textContent = `R$ ${subtotal.toFixed(2).replace('.', ',')}`;
            mobileSubtotalEl.textContent = `R$ ${subtotal.toFixed(2).replace('.', ',')}`;
            
            // Validate form
            validateForm();
        }

        function renderCartItems() {
            // Desktop cart
            if (cart.length === 0) {
                cartItemsEl.innerHTML = '<p class="text-gray-500 dark:text-gray-400 text-center py-4">Seu carrinho está vazio</p>';
                mobileCartItemsEl.innerHTML = '<p class="text-gray-500 dark:text-gray-400 text-center py-4">Seu carrinho está vazio</p>';
                return;
            }
            
            cartItemsEl.innerHTML = '';
            mobileCartItemsEl.innerHTML = '';
            
            cart.forEach((item, index) => {
                const itemEl = document.createElement('div');
                itemEl.className = 'flex justify-between items-center py-3 border-b dark:border-gray-700 cart-item';
                itemEl.innerHTML = `
                    <div>
                        <h4 class="font-medium">${item.name}</h4>
                        <div class="flex items-center mt-1">
                            <button class="quantity-btn text-sm px-2 py-1 bg-gray-200 dark:bg-gray-700 rounded" data-index="${index}" data-action="decrease">-</button>
                            <span class="mx-2">${item.quantity}</span>
                            <button class="quantity-btn text-sm px-2 py-1 bg-gray-200 dark:bg-gray-700 rounded" data-index="${index}" data-action="increase">+</button>
                            <span class="ml-4 font-semibold">R$ ${(item.price * item.quantity).toFixed(2).replace('.', ',')}</span>
                        </div>
                    </div>
                    <button class="remove-btn text-red-500 hover:text-red-700" data-index="${index}">
                        <i class="fas fa-trash"></i>
                    </button>
                `;
                cartItemsEl.appendChild(itemEl.cloneNode(true));
                mobileCartItemsEl.appendChild(itemEl);
            });
            
            // Add event listeners to quantity and remove buttons
            document.querySelectorAll('.quantity-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const index = parseInt(e.target.dataset.index);
                    const action = e.target.dataset.action;
                    
                    if (action === 'increase') {
                        cart[index].quantity += 1;
                    } else if (action === 'decrease') {
                        if (cart[index].quantity > 1) {
                            cart[index].quantity -= 1;
                        } else {
                            removeFromCart(index);
                            return;
                        }
                    }
                    
                    updateCart();
                });
            });
            
            document.querySelectorAll('.remove-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const index = parseInt(e.target.dataset.index);
                    removeFromCart(index);
                });
            });
        }

        // Form validation
        function validateForm() {
            const name = customerNameEl.value.trim() || mobileCustomerNameEl.value.trim();
            const address = customerAddressEl.value.trim() || mobileCustomerAddressEl.value.trim();
            const hasItems = cart.length > 0;
            
            const isValid = name && address && hasItems;
            
            sendOrderBtn.disabled = !isValid;
            mobileSendOrderBtn.disabled = !isValid;
            
            if (isValid) {
                sendOrderBtn.classList.remove('bg-gray-300', 'text-gray-600');
                sendOrderBtn.classList.add('bg-green-500', 'hover:bg-green-600', 'text-white');
                mobileSendOrderBtn.classList.remove('bg-gray-300', 'text-gray-600');
                mobileSendOrderBtn.classList.add('bg-green-500', 'hover:bg-green-600', 'text-white');
            } else {
                sendOrderBtn.classList.add('bg-gray-300', 'text-gray-600');
                sendOrderBtn.classList.remove('bg-green-500', 'hover:bg-green-600', 'text-white');
                mobileSendOrderBtn.classList.add('bg-gray-300', 'text-gray-600');
                mobileSendOrderBtn.classList.remove('bg-green-500', 'hover:bg-green-600', 'text-white');
            }
        }

        // Send order
        function sendOrder() {
            const name = customerNameEl.value.trim() || mobileCustomerNameEl.value.trim();
            const address = customerAddressEl.value.trim() || mobileCustomerAddressEl.value.trim();
            
            if (!name || !address || cart.length === 0) return;
            
            // Format order message
            let message = `Olá, este é o meu pedido de hoje!\n\n`;
            message += `*Nome:* ${name}\n`;
            message += `*Endereço:* ${address}\n\n`;
            message += `*Itens do pedido:*\n`;
            
            cart.forEach(item => {
                message += `- ${item.name} x${item.quantity} - R$ ${(item.price * item.quantity).toFixed(2).replace('.', ',')}\n`;
            });
            
            const subtotal = cart.reduce((total, item) => total + (item.price * item.quantity), 0);
            message += `\n*Total:* R$ ${subtotal.toFixed(2).replace('.', ',')}\n\n`;
            message += `Horário do pedido: ${new Date().toLocaleString()}`;
            
            // Encode for WhatsApp URL
            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://wa.me/5538998722422?text=${encodedMessage}`;
            
            // Open WhatsApp
            window.open(whatsappUrl, '_blank');
            
            // Clear cart
            cart = [];
            updateCart();
            customerNameEl.value = '';
            customerAddressEl.value = '';
            mobileCustomerNameEl.value = '';
            mobileCustomerAddressEl.value = '';
            
            // Show success message
            alert('Pedido enviado com sucesso! Você será redirecionado para o WhatsApp.');
        }

        // Theme functions
        function checkThemePreference() {
            if (localStorage.getItem('darkMode') === 'true' || 
                (!localStorage.getItem('darkMode') && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        }

        function toggleTheme() {
            const isDark = document.documentElement.classList.toggle('dark');
            localStorage.setItem('darkMode', isDark);
        }
    </script>
</body>
</html>
