<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Las Gemelas | Tienda en Linea</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* =========================================
           VARIABLES DE COLORES Y DISENO
           ========================================= */
        :root {
            --brand-gradient: linear-gradient(135deg, #B39DDB, #F48FB1);
            --primary: #D81B60; 
            --primary-hover: #AD1457;
            --surface-dark: #111827; 
            
            --header-bg: #FCE4EC; 
            --header-text: #4A148C; 
            
            --bg-app: #FDFEFE;
            --white: #FFFFFF;
            --text-main: #1F2937;
            --text-muted: #6B7280;
            --border-color: #F3E5F5; 
            --success: #10B981;
            --danger: #EF4444;
            --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
            --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.05);
            --radius-lg: 16px;
        }

        * { box-sizing: border-box; }
        body { font-family: 'Poppins', sans-serif; margin: 0; padding: 0; background-color: var(--bg-app); color: var(--text-main); }
        input[type="number"]::-webkit-inner-spin-button, input[type="number"]::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
        input[type="number"] { -moz-appearance: textfield; }

        header {
            background: var(--header-bg); padding: 0 40px; display: flex; justify-content: space-between;
            align-items: center; height: 80px; position: sticky; top: 0; z-index: 100;
            box-shadow: 0 4px 15px rgba(74, 20, 140, 0.1); 
        }

        .brand { display: flex; align-items: center; gap: 15px; font-size: 24px; font-weight: 800; color: var(--header-text); letter-spacing: 0.5px; }
        .brand img { height: 45px; width: 45px; object-fit: cover; border-radius: 10px; box-shadow: 0 0 10px rgba(74, 20, 140, 0.2); }

        nav { display: flex; gap: 10px; height: 100%; }
        nav button { background: transparent; border: none; color: #7B1FA2; padding: 0 20px; font-family: inherit; font-size: 15px; font-weight: 600; cursor: pointer; height: 100%; display: flex; align-items: center; gap: 8px; position: relative; transition: all 0.3s; }
        nav button:hover { color: var(--primary); }
        nav button.active { color: var(--primary); font-weight: 700; }
        nav button.active::after { content: ''; position: absolute; bottom: 0; left: 0; width: 100%; height: 4px; background: var(--brand-gradient); border-radius: 4px 4px 0 0; }

        /* Estilo especial para el boton de cerrar sesion */
        #btn-logout { background-color: var(--danger); color: white; border-radius: 8px; height: 70%; margin-top: 10px; padding: 0 15px; }
        #btn-logout:hover { background-color: #B91C1C; color: white; }
        #btn-logout::after { display: none; }

        .hero {
            position: relative; height: 280px; border-radius: var(--radius-lg); margin-bottom: 40px;
            overflow: hidden; display: flex; flex-direction: column; justify-content: center; padding: 0 60px;
            background-image: url('https://www.novaclean.es/wp-content/uploads/2026/02/SERVICIOS-VENTA-DE-PRODUCTOS-Y-ACCESORIOS-DE-LIMPIEZA-E-HIGIENE-1024x683.webp');
            background-size: cover; background-position: center; box-shadow: var(--shadow-lg);
        }
        .hero::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: linear-gradient(to right, rgba(106, 27, 154, 0.85) 0%, rgba(156, 39, 176, 0.5) 100%); }
        .hero h1 { margin: 0; font-size: 42px; font-weight: 800; color: var(--white); position: relative; z-index: 2; text-shadow: 2px 2px 4px rgba(0,0,0,0.3); }
        .hero p { margin: 15px 0 0 0; font-size: 18px; color: #F3E5F5; max-width: 600px; line-height: 1.6; position: relative; z-index: 2; }

        main { padding: 40px 30px; max-width: 1350px; margin: auto; }
        .view { display: none; animation: fadeIn 0.4s ease; }
        .view.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

        .section-header { margin-bottom: 25px; border-left: 5px solid var(--primary); padding-left: 15px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 15px; }
        .section-header h2 { margin: 0; font-size: 26px; font-weight: 700; color: var(--header-text);}
        .search-container { position: relative; width: 100%; max-width: 400px; }
        .search-icon { position: absolute; left: 15px; top: 50%; transform: translateY(-50%); color: var(--text-muted); font-size: 18px; }
        #pos-search { width: 100%; padding: 12px 15px 12px 45px; border: 2px solid var(--border-color); border-radius: 10px; font-size: 15px; font-family: inherit; color: var(--text-main); outline: none; transition: all 0.3s; box-shadow: var(--shadow-md); }
        #pos-search:focus { border-color: var(--primary); box-shadow: 0 0 0 4px rgba(216, 27, 96, 0.15); }

        .layout-split { display: grid; grid-template-columns: 1fr 350px; gap: 30px; align-items: start; }
        
        /* Auto-fit asegura que las tarjetas siempre se estiren para rellenar los espacios en blanco */
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }

        .card { background: var(--white); border-radius: var(--radius-lg); border: 1px solid var(--border-color); box-shadow: var(--shadow-md); transition: all 0.3s; display: flex; flex-direction: column; overflow: hidden; }
        .card:hover { box-shadow: 0 15px 25px rgba(216, 27, 96, 0.1); transform: translateY(-5px); border-color: var(--primary);}
        .card-img-container { width: 100%; height: 180px; overflow: hidden; background-color: #f8f9fa; }
        .card-img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.5s ease; }
        .card:hover .card-img { transform: scale(1.05); }
        .card-content { padding: 15px; flex-grow: 1; display: flex; flex-direction: column; }
        .card h3 { margin: 0 0 5px 0; font-size: 16px; font-weight: 700; color: var(--header-text); }
        .card .stock { font-size: 13px; color: var(--text-muted); margin-bottom: 10px; }
        .card .price { font-size: 22px; font-weight: 800; color: var(--primary); margin: 0 0 12px 0; }

        .qty-wrapper { display: flex; align-items: center; background: #FCE4EC; border-radius: 8px; padding: 5px; margin-bottom: 12px; border: 1px solid var(--border-color);}
        .qty-label { font-size: 12px; font-weight: 600; color: var(--header-text); padding: 0 8px; text-transform: uppercase;}
        .qty-wrapper input { flex: 1; border: none; background: transparent; text-align: center; font-size: 15px; font-weight: 700; color: var(--text-main); height: 30px; outline: none; }

        .btn { border: none; border-radius: 10px; cursor: pointer; font-weight: 600; font-size: 14px; padding: 12px 15px; transition: all 0.2s; display: flex; align-items: center; justify-content: center; gap: 8px; width: 100%; font-family: inherit; }
        .btn-add { background: var(--brand-gradient); color: var(--white); margin-top: auto; }
        .btn-add:hover:not([disabled]) { box-shadow: 0 5px 15px rgba(216, 27, 96, 0.3); transform: scale(1.02);}
        .btn-add[disabled] { background: #E5E7EB; color: #9CA3AF; cursor: not-allowed; box-shadow: none; transform: none;}
        .btn-whatsapp { background: var(--success); color: var(--white); font-size: 16px; padding: 16px; }
        .btn-whatsapp:hover { background: #059669; box-shadow: 0 6px 15px rgba(16,185,129,0.3); }

        .side-panel { background: var(--white); border-radius: var(--radius-lg); box-shadow: var(--shadow-lg); padding: 20px; position: sticky; top: 100px; border: 1px solid var(--border-color);}
        .side-panel h3 { margin: 0 0 15px 0; font-size: 18px; color: var(--header-text); display: flex; align-items: center; gap: 10px; padding-bottom: 12px; border-bottom: 2px solid var(--border-color);}
        .items-list { max-height: 350px; overflow-y: auto; margin-bottom: 15px; padding-right: 5px;}
        .items-list::-webkit-scrollbar { width: 4px; }
        .items-list::-webkit-scrollbar-thumb { background-color: #F48FB1; border-radius: 4px; }
        .list-item { display: flex; justify-content: space-between; align-items: center; padding: 12px 0; border-bottom: 1px dashed var(--border-color); }
        .list-item:last-child { border-bottom: none; }
        .cart-item-img { width: 45px; height: 45px; border-radius: 8px; object-fit: cover; margin-right: 10px; }
        .item-info-row { display: flex; align-items: center; }
        .item-name { font-size: 13px; font-weight: 700; color: var(--text-main); display: block; margin-bottom: 2px; line-height: 1.2;}
        .item-total { font-weight: 800; color: var(--primary); font-size: 15px;}

        /* Nuevos estilos para los controles de cantidad dentro del carrito */
        .cart-controls { display: flex; align-items: center; gap: 6px; margin-top: 5px; }
        .btn-cart-qty { background: var(--bg-app); border: 1px solid var(--border-color); border-radius: 4px; width: 22px; height: 22px; display: flex; align-items: center; justify-content: center; cursor: pointer; color: var(--header-text); font-weight: bold; font-size: 12px; transition: all 0.2s;}
        .btn-cart-qty:hover { background: var(--border-color); }
        .btn-cart-remove { background: none; border: none; color: var(--danger); cursor: pointer; font-size: 14px; padding: 4px; margin-left: 5px; transition: color 0.2s;}
        .btn-cart-remove:hover { color: #B91C1C; transform: scale(1.1);}

        .summary-row { display: flex; justify-content: space-between; align-items: flex-end; padding: 15px 0; border-top: 3px solid var(--border-color); margin-bottom: 10px; }
        .summary-label { font-size: 14px; font-weight: 700; color: var(--text-muted); text-transform: uppercase;}
        .summary-total { font-size: 28px; font-weight: 800; color: var(--header-text); line-height: 1;}

        .fab { position: fixed; bottom: 30px; right: 30px; width: 60px; height: 60px; background: var(--brand-gradient); color: var(--white); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 24px; box-shadow: 0 10px 25px rgba(216, 27, 96, 0.4); cursor: pointer; transition: all 0.3s; z-index: 1000; }
        .fab:hover { transform: scale(1.1) translateY(-5px); }
        .badge { position: absolute; top: -2px; right: -2px; background: var(--surface-dark); color: var(--white); font-size: 12px; font-weight: 800; width: 24px; height: 24px; border-radius: 50%; display: flex; align-items: center; justify-content: center; border: 2px solid var(--white); }

        .modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(74, 20, 140, 0.5); backdrop-filter: blur(4px); z-index: 999; opacity: 0; transition: opacity 0.3s; }
        .modal-overlay.show { display: block; opacity: 1; }
        .modal { position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%) scale(0.95); width: 90%; max-width: 400px; z-index: 1000; display: none; opacity: 0; transition: all 0.3s; }
        .modal.show { display: block; opacity: 1; transform: translate(-50%, -50%) scale(1); }

        .secret-trigger { position: fixed; bottom: 15px; left: 15px; color: rgba(0, 0, 0, 0.04); font-size: 22px; cursor: pointer; z-index: 100; transition: color 0.3s; }
        .secret-trigger:hover { color: rgba(216, 27, 96, 0.3); } 

        .login-input { width: 100%; padding: 12px; border: 2px solid var(--border-color); border-radius: 10px; margin-bottom: 20px; font-size: 15px; font-family: inherit; outline: none; transition: border-color 0.3s; text-align: center; }
        .login-input:focus { border-color: var(--primary); }

        .toast { position: fixed; bottom: -80px; left: 50%; transform: translateX(-50%); background: var(--header-text); color: var(--white); padding: 12px 25px; border-radius: 10px; font-size: 14px; font-weight: 600; box-shadow: 0 10px 30px rgba(0,0,0,0.2); transition: bottom 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); z-index: 2000; display: flex; align-items: center; gap: 10px; }
        .toast.show { bottom: 30px; }

        @media (max-width: 768px) {
            header { padding: 10px 20px; height: auto; flex-direction: column; gap: 10px; }
            .brand { font-size: 20px; }
            .brand img { width: 35px; height: 35px; }
            nav button { padding: 10px; font-size: 14px; }
            main { padding: 20px 15px; }
            .hero { padding: 0 20px; height: 200px; margin-bottom: 25px; }
            .hero h1 { font-size: 28px; }
            .hero p { font-size: 14px; }
            .section-header h2 { font-size: 20px; }
            .search-container { max-width: 100%; }
            .layout-split { grid-template-columns: 1fr; gap: 20px; }
            .side-panel { position: relative; top: 0; }
            .grid { grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 15px;}
            .card-img-container { height: 140px; }
            .card .price { font-size: 18px; }
            .qty-wrapper input { font-size: 14px; height: 25px; }
            .btn-add { padding: 10px; font-size: 12px; }
            .fab { bottom: 20px; right: 20px; width: 55px; height: 55px; font-size: 20px; }
        }

        .loader-container { text-align: center; padding: 50px; grid-column: 1 / -1; color: var(--header-text); font-weight: 600;}
    </style>
</head>
<body>

    <header>
        <div class="brand">
            <img id="logo-img" src="https://cdn-icons-png.flaticon.com/256/17225/17225675.png" alt="Logotipo">
            Las Gemelas
        </div>
        <nav>
            <button id="btn-store" onclick="tryGoStore()">
                <i class="fa-solid fa-store"></i> Tienda en Linea
            </button>
            
            <button id="btn-logout" style="display: none;" onclick="logoutPOS()">
                <i class="fa-solid fa-right-from-bracket"></i> Cerrar Sesion
            </button>
        </nav>
    </header>

    <i class="fa-solid fa-fingerprint secret-trigger" onclick="openLoginModal()" title="Acceso de Personal"></i>

    <main>
        <section id="store" class="view active">
            <div class="hero">
                <h1>Limpieza para tu Hogar</h1>
                <p>Abastece tus espacios con la mejor calidad en jarceria y quimicos. Haz tu pedido y recibelo facilmente.</p>
            </div>

            <div class="section-header">
                <h2>Catalogo de Productos</h2>
            </div>
            
            <div class="grid" id="store-grid">
                <div class="loader-container"><i class="fa-solid fa-spinner fa-spin fa-2x"></i><br><br>Cargando productos de la base de datos...</div>
            </div>

            <div class="fab" onclick="toggleCartModal()">
                <i class="fa-solid fa-cart-shopping"></i>
                <span class="badge" id="web-cart-badge">0</span>
            </div>
        </section>

        <section id="pos" class="view">
            <div class="section-header">
                <h2>Caja Rapida en Mostrador</h2>
                <div class="search-container">
                    <i class="fa-solid fa-magnifying-glass search-icon"></i>
                    <input type="text" id="pos-search" placeholder="Buscar producto o SKU (#001)..." onkeyup="filterPOSProducts()">
                </div>
            </div>

            <div class="layout-split">
                <div class="grid" id="pos-grid">
                    </div>
                
                <div class="side-panel">
                    <h3><i class="fa-solid fa-receipt" style="color: var(--primary);"></i> Ticket de Venta</h3>
                    <div class="items-list" id="pos-cart-items">
                        <p style="color: var(--text-muted); text-align:center; padding: 20px 0; font-weight: 500;">Escanee un producto.</p>
                    </div>
                    <div class="summary-row">
                        <span class="summary-label">Cobro Total</span>
                        <span class="summary-total">$<span id="pos-cart-total">0.00</span></span>
                    </div>
                    <button class="btn" style="background: var(--header-text); color: white; padding: 15px; font-size: 16px;" onclick="checkoutPOS()" id="btn-cobrar">
                        <i class="fa-solid fa-print"></i> Cobrar e Imprimir
                    </button>
                </div>
            </div>
        </section>
    </main>

    <div class="modal-overlay" id="modal-overlay" onclick="closeAllModals()"></div>

    <div class="modal" id="cart-modal">
        <div class="side-panel" style="margin:0; box-shadow:none;">
            <h3><i class="fa-solid fa-bag-shopping" style="color: var(--primary);"></i> Resumen de Pedido</h3>
            <div class="items-list" id="web-cart-items"></div>
            <div class="summary-row">
                <span class="summary-label">Total a Pagar</span>
                <span class="summary-total">$<span id="web-cart-total">0.00</span></span>
            </div>
            <div style="display:flex; flex-direction:column; gap:10px; margin-top: 5px;">
                <button class="btn btn-whatsapp" onclick="sendWhatsAppOrder()">
                    <i class="fa-brands fa-whatsapp" style="font-size: 20px;"></i> Enviar por WhatsApp
                </button>
                <button class="btn" style="background: var(--border-color); color: var(--header-text);" onclick="closeAllModals()">Seguir Comprando</button>
            </div>
        </div>
    </div>

    <div class="modal" id="login-modal">
        <div class="side-panel" style="margin:0; box-shadow:none; text-align: center;">
            <h3><i class="fa-solid fa-lock" style="color: var(--primary);"></i> Acceso a Caja (POS)</h3>
            <p style="color: var(--text-muted); font-size: 13px; margin-bottom: 20px;">Area restringida solo para personal autorizado.</p>
            <input type="password" id="pos-password" class="login-input" placeholder="Ingresa la contrasena..." onkeyup="if(event.key === 'Enter') verifyPassword()">
            <div style="display:flex; gap:10px;">
                <button class="btn" style="background: var(--header-text); color: white;" onclick="verifyPassword()">Ingresar</button>
                <button class="btn" style="background: var(--border-color); color: var(--header-text);" onclick="closeAllModals()">Cancelar</button>
            </div>
        </div>
    </div>

    <div id="toast" class="toast">
        <i class="fa-solid fa-circle-check" style="color: var(--success); font-size: 20px;"></i>
        <span id="toast-msg">Operacion completada</span>
    </div>

    <script>
        // =========================================================================
        // VARIABLES GLOBALES
        // =========================================================================
        
        // AQUI PEGAS LA URL DE TU WEB APP SCRIPT (Conecta tu web con Google Sheets)
        const APP_SCRIPT_URL = "https://script.google.com/macros/s/AKfycby7PzsczJNau9ZZZdKAJnm8qY5qnDUeof2aMRf5HTRoRoBWQvHio7LAUCU8Ph5E_1sU/exec"; 

        // AQUI PONES TU NUMERO DE WHATSAPP (A donde llegaran los pedidos web)
        const WHATSAPP_NUMBER = "521234567890"; 
        
        // AQUI PONES LA CONTRASENA PARA ENTRAR A LA CAJA
        const POS_PASSWORD = "admin123";

        let products = []; 
        let webCart = []; 
        let posCart = []; 

        // =========================================================================
        // CONEXION A LA BASE DE DATOS (GOOGLE SHEETS)
        // =========================================================================
        
        // Funcion: Descarga el inventario de Google Sheets a la pagina
        async function fetchProducts() {
            try {
                const response = await fetch(APP_SCRIPT_URL);
                products = await response.json();
                renderCatalogs();
            } catch (error) {
                console.error("Error al cargar base de datos:", error);
                document.getElementById('store-grid').innerHTML = '<p style="text-align:center; width:100%; color:red;">No se pudo conectar a la base de datos.</p>';
            }
        }

        // =========================================================================
        // FUNCIONES DE CONTROL DE VISTAS Y ACCESO
        // =========================================================================
        
        // Funcion: Bloquea el boton de Tienda cuando el cajero esta logueado
        function tryGoStore() {
            // Si la memoria del navegador dice que hay sesion activa, no hace nada
            if(localStorage.getItem('pos_logged_in') === 'true') {
                return;
            }
            switchView('store');
        }

        // Funcion: Cambia la pantalla visible entre la Tienda Publica y la Caja Privada
        function switchView(viewName) {
            document.querySelectorAll('.view').forEach(el => el.classList.remove('active'));
            document.getElementById(viewName).classList.add('active');
            
            // Logica para cambiar el menu dependiendo si es tienda o es caja
            if(viewName === 'pos') {
                document.getElementById('btn-store').classList.remove('active');
                document.getElementById('btn-store').style.opacity = '0.5'; // Hace que el icono tienda se vea apagado
                document.getElementById('btn-store').style.cursor = 'default';
                document.getElementById('btn-logout').style.display = 'flex'; // Aparece boton rojo de cerrar sesion
                document.querySelector('.secret-trigger').style.display = 'none'; // Oculta huella dactilar
            } else {
                document.getElementById('btn-store').classList.add('active');
                document.getElementById('btn-store').style.opacity = '1';
                document.getElementById('btn-store').style.cursor = 'pointer';
                document.getElementById('btn-logout').style.display = 'none'; // Oculta boton de cerrar sesion
                document.querySelector('.secret-trigger').style.display = 'block'; // Muestra huella dactilar
            }
            closeAllModals();
        }

        // Funcion: Muestra la ventana para teclear la contrasena
        function openLoginModal() {
            document.getElementById('login-modal').classList.add('show');
            document.getElementById('modal-overlay').classList.add('show');
            document.getElementById('pos-password').value = '';
            document.getElementById('pos-password').focus();
        }

        // Funcion: Verifica que la clave coincida y guarda la sesion para no cerrarse al recargar
        function verifyPassword() {
            const passInput = document.getElementById('pos-password');
            if (passInput.value === POS_PASSWORD) {
                closeAllModals(); 
                localStorage.setItem('pos_logged_in', 'true'); // Guarda un archivo en memoria indicando que ingreso con exito
                switchView('pos'); 
                passInput.value = ''; 
                showToast("Acceso autorizado a Caja");
            } else {
                alert("Contrasena incorrecta. Acceso denegado.");
            }
        }

        // Funcion: Borra la sesion guardada y te regresa a la tienda online
        function logoutPOS() {
            localStorage.removeItem('pos_logged_in'); // Borra la memoria
            posCart = []; // Borra lo que haya en la caja por seguridad
            updatePOSCartUI();
            switchView('store');
            showToast("Sesion cerrada correctamente");
        }

        // Funcion: Dibuja un cartel verde pequeno cuando se hace una accion
        function showToast(message) {
            const toast = document.getElementById("toast");
            document.getElementById("toast-msg").innerText = message;
            toast.classList.add("show");
            setTimeout(() => toast.classList.remove("show"), 3000);
        }

        // =========================================================================
        // CREACION VISUAL DEL CATALOGO (TARJETAS DE PRODUCTOS)
        // =========================================================================
        
        // Funcion: Imprime el listado de productos como cajitas interactivas
        function renderCatalogs() {
            const storeGrid = document.getElementById('store-grid');
            const posGrid = document.getElementById('pos-grid');
            storeGrid.innerHTML = ''; posGrid.innerHTML = '';

            products.forEach(p => {
                const isOutOfStock = p.stock <= 0;
                const buttonStatus = isOutOfStock ? 'disabled' : '';
                const btnTextStore = isOutOfStock ? 'Agotado' : '<i class="fa-solid fa-cart-plus"></i> Agregar';
                const btnTextPOS = isOutOfStock ? 'Agotado' : '<i class="fa-solid fa-barcode"></i> Registrar';
                
                const cardHTML = (viewType) => `
                    <div class="card" data-name="${p.name.toLowerCase()}" data-id="${p.id}">
                        <div class="card-img-container">
                            <img src="${p.image}" class="card-img" alt="${p.name}" onerror="this.src='https://via.placeholder.com/400x300?text=Sin+Imagen'">
                        </div>
                        <div class="card-content">
                            <h3>${p.name}</h3>
                            <div class="stock">Disponibles: <b>${p.stock} pzas</b></div>
                            <div class="price">$${parseFloat(p.price).toFixed(2)}</div>
                            
                            <div class="qty-wrapper">
                                <span class="qty-label">Cant.</span>
                                <input type="number" id="${viewType}-qty-${p.id}" value="1" min="1" max="${p.stock}" ${buttonStatus}>
                            </div>
                            
                            <button class="btn btn-add" onclick="add${viewType === 'web' ? 'ToWebCart' : 'ToPOSCart'}(${p.id})" ${buttonStatus}>
                                ${viewType === 'web' ? btnTextStore : btnTextPOS}
                            </button>
                        </div>
                    </div>
                `;

                storeGrid.innerHTML += cardHTML('web');
                posGrid.innerHTML += cardHTML('pos');
            });
        }

        // Funcion: Filtra y oculta productos en la caja registradora cuando usas la barra de busqueda
        function filterPOSProducts() {
            const query = document.getElementById('pos-search').value.toLowerCase();
            const cards = document.querySelectorAll('#pos-grid .card');
            cards.forEach(card => {
                const name = card.getAttribute('data-name');
                const id = card.getAttribute('data-id');
                if (name.includes(query) || id.includes(query) || ("00"+id).includes(query) || ("#00"+id).includes(query)) {
                    card.style.display = 'flex';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // =========================================================================
        // FUNCIONES MODIFICACION Y ELIMINACION EN CARRITO
        // =========================================================================
        
        // Funcion: Cambia la cantidad de un producto (+ o -) directamente desde la ventana del carrito
        function changeQty(cartType, productId, changeAmount) {
            // Selecciona si modificamos la tienda (webCart) o la caja registradora (posCart)
            let cart = cartType === 'web' ? webCart : posCart;
            const itemIndex = cart.findIndex(item => item.id == productId);
            
            if (itemIndex === -1) return; // Si no existe, no hace nada

            const p = products.find(x => x.id == productId);
            let newQty = cart[itemIndex].qty + changeAmount;

            // Si la cantidad llega a 0, lo elimina por completo del carrito
            if (newQty <= 0) {
                removeCartItem(cartType, productId);
                return;
            }

            // Evita que el cliente pida mas productos de los que existen en el inventario
            if (newQty > p.stock) {
                alert(`No hay mas unidades en existencia. Disponibles: ${p.stock}`);
                return;
            }

            // Actualiza la cantidad y vuelve a dibujar el carrito
            cart[itemIndex].qty = newQty;
            if (cartType === 'web') updateWebCartUI();
            else updatePOSCartUI();
        }

        // Funcion: Elimina el producto por completo cuando se presiona el bote de basura
        function removeCartItem(cartType, productId) {
            if (cartType === 'web') {
                webCart = webCart.filter(item => item.id != productId);
                updateWebCartUI();
            } else {
                posCart = posCart.filter(item => item.id != productId);
                updatePOSCartUI();
            }
        }

        // =========================================================================
        // FUNCIONES DE LA TIENDA WEB
        // =========================================================================
        
        // Funcion: Abre y cierra la ventana visual del carrito web
        function toggleCartModal() {
            document.getElementById('cart-modal').classList.toggle('show');
            document.getElementById('modal-overlay').classList.toggle('show');
        }
        
        // Funcion: Cierra por la fuerza cualquier mensaje emergente abierto
        function closeAllModals() {
            document.getElementById('cart-modal').classList.remove('show');
            document.getElementById('login-modal').classList.remove('show');
            document.getElementById('modal-overlay').classList.remove('show');
        }

        // Funcion: Envia un producto al carrito de internet validando la cantidad solicitada
        function addToWebCart(productId) {
            const p = products.find(x => x.id == productId);
            const input = document.getElementById(`web-qty-${productId}`);
            const qty = parseInt(input.value);

            if (isNaN(qty) || qty <= 0) return;

            const cartItem = webCart.find(item => item.id == productId);
            const currentQty = cartItem ? cartItem.qty : 0;

            if (currentQty + qty <= p.stock) {
                if (cartItem) cartItem.qty += qty;
                else webCart.push({ ...p, qty: qty });
                
                showToast(`Se agrego ${p.name} al carrito`);
                input.value = 1;
                updateWebCartUI();
            } else {
                alert(`No hay mas unidades. Disponibles: ${p.stock - currentQty}`);
            }
        }

        // Funcion: Refresca el contenido visual del carrito (Ahora incluye los botones de modificar cantidad y eliminar)
        function updateWebCartUI() {
            const container = document.getElementById('web-cart-items');
            let total = 0, items = 0;
            container.innerHTML = '';

            if (webCart.length === 0) {
                container.innerHTML = '<p style="text-align:center;">Tu carrito esta vacio.</p>';
            } else {
                webCart.forEach(item => {
                    let sub = item.price * item.qty;
                    total += sub; items += item.qty;
                    container.innerHTML += `
                        <div class="list-item" style="flex-direction: column; align-items: flex-start;">
                            <div class="item-info-row" style="width: 100%; justify-content: space-between;">
                                <div style="display: flex; align-items: center;">
                                    <img src="${item.image}" class="cart-item-img">
                                    <div>
                                        <span class="item-name">${item.name}</span>
                                    </div>
                                </div>
                                <span class="item-total">$${sub.toFixed(2)}</span>
                            </div>
                            <div class="cart-controls">
                                <button class="btn-cart-qty" onclick="changeQty('web', ${item.id}, -1)">-</button>
                                <span style="font-size: 13px; font-weight: bold; width: 18px; text-align: center;">${item.qty}</span>
                                <button class="btn-cart-qty" onclick="changeQty('web', ${item.id}, 1)">+</button>
                                <button class="btn-cart-remove" onclick="removeCartItem('web', ${item.id})" title="Eliminar"><i class="fa-solid fa-trash"></i></button>
                            </div>
                        </div>
                    `;
                });
            }
            document.getElementById('web-cart-total').innerText = total.toFixed(2);
            document.getElementById('web-cart-badge').innerText = items;
        }

        // Funcion: Une todos los datos del pedido en un texto plano y lo manda al WhatsApp configurado
        function sendWhatsAppOrder() {
            if (webCart.length === 0) { alert("El carrito esta vacio."); return; }

            let text = "*✨ Pedido Web | Las Gemelas ✨*\n----------------------------------------\n";
            let total = 0;

            webCart.forEach(item => {
                let sub = item.qty * item.price;
                total += sub;
                text += `▪️ ${item.qty}x ${item.name} ($${sub.toFixed(2)})\n`;
            });

            text += `----------------------------------------\n*Total a pagar: $${total.toFixed(2)}*\n\nPor favor, confirmar pedido.`;
            window.open(`https://wa.me/${WHATSAPP_NUMBER}?text=${encodeURIComponent(text)}`, '_blank');
        }

        // =========================================================================
        // FUNCIONES DEL PUNTO DE VENTA (CAJERO) Y TICKETS
        // =========================================================================
        
        // Funcion: Añade productos al ticket fiscal del establecimiento
        function addToPOSCart(productId) {
            const p = products.find(x => x.id == productId);
            const input = document.getElementById(`pos-qty-${productId}`);
            const qty = parseInt(input.value);

            if (isNaN(qty) || qty <= 0) return;

            const cartItem = posCart.find(item => item.id == productId);
            const currentQty = cartItem ? cartItem.qty : 0;

            if (currentQty + qty <= p.stock) {
                if (cartItem) cartItem.qty += qty;
                else posCart.push({ ...p, qty: qty });
                
                input.value = 1;
                updatePOSCartUI();
            } else {
                alert(`No hay stock suficiente para este producto.`);
            }
        }

        // Funcion: Pinta la lista que ve el cajero (Ahora incluye botones para borrar errores al cobrar)
        function updatePOSCartUI() {
            const container = document.getElementById('pos-cart-items');
            let total = 0;
            container.innerHTML = '';

            if (posCart.length === 0) {
                container.innerHTML = '<p style="text-align:center;">Escanee un producto.</p>';
            } else {
                posCart.forEach(item => {
                    let sub = item.price * item.qty;
                    total += sub;
                    container.innerHTML += `
                        <div class="list-item" style="flex-direction: column; align-items: flex-start;">
                            <div class="item-info-row" style="width: 100%; justify-content: space-between;">
                                <div style="display: flex; align-items: center;">
                                    <img src="${item.image}" class="cart-item-img">
                                    <div>
                                        <span class="item-name">${item.name}</span>
                                    </div>
                                </div>
                                <span class="item-total">$${sub.toFixed(2)}</span>
                            </div>
                            <div class="cart-controls">
                                <button class="btn-cart-qty" onclick="changeQty('pos', ${item.id}, -1)">-</button>
                                <span style="font-size: 13px; font-weight: bold; width: 18px; text-align: center;">${item.qty}</span>
                                <button class="btn-cart-qty" onclick="changeQty('pos', ${item.id}, 1)">+</button>
                                <button class="btn-cart-remove" onclick="removeCartItem('pos', ${item.id})" title="Eliminar"><i class="fa-solid fa-trash"></i></button>
                            </div>
                        </div>
                    `;
                });
            }
            document.getElementById('pos-cart-total').innerText = total.toFixed(2);
        }

        // Funcion: Genera el texto plano que sera convertido en un documento de bloc de notas
        function generateTicketText(cart, total) {
            let now = new Date();
            let dateStr = now.toLocaleDateString('es-MX') + ' ' + now.toLocaleTimeString('es-MX');
            
            let text = "========================================\n";
            text += "         LAS GEMELAS - SUCURSAL         \n";
            text += "========================================\n";
            text += `Fecha : ${dateStr}\n`;
            text += "----------------------------------------\n";
            text += "Cant.  Articulo                 Subtotal\n";
            text += "----------------------------------------\n";
            
            cart.forEach(item => {
                let sub = item.qty * item.price;
                let name = item.name.length > 20 ? item.name.substring(0, 20) + ".." : item.name.padEnd(22, ' ');
                text += `${item.qty.toString().padEnd(6, ' ')} ${name} $${sub.toFixed(2)}\n`;
            });
            
            text += "----------------------------------------\n";
            text += `TOTAL A COBRAR:                 $${total.toFixed(2)}\n`;
            text += "========================================\n";
            text += "        ¡Gracias por su compra!         \n";
            
            return text;
        }

        // Funcion: Forza a la computadora a guardar el archivo TXT para imprimirlo despues
        function downloadTicket(text) {
            const blob = new Blob([text], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            
            let now = new Date();
            let timeStamp = now.toISOString().replace(/[:\-T]/g, '').substring(0, 14);
            
            a.href = url;
            a.download = `Ticket_LasGemelas_${timeStamp}.txt`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        // Funcion: Comunica el cobro a Google Sheets y vacia el ticket para la proxima venta
        async function checkoutPOS() {
            if (posCart.length === 0) { alert("Ticket vacio. Agregue productos."); return; }
            if (APP_SCRIPT_URL === "URL_DE_TU_APP_SCRIPT_AQUI") {
                alert("Debes poner la URL de App Script en el codigo antes de cobrar."); return;
            }

            const btnCobrar = document.getElementById('btn-cobrar');
            btnCobrar.innerText = "Procesando...";
            btnCobrar.disabled = true;

            let total = 0;
            const payload = posCart.map(item => {
                total += (item.qty * item.price);
                return { id: item.id, qty: item.qty };
            });

            try {
                await fetch(APP_SCRIPT_URL, {
                    method: 'POST',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify(payload)
                });

                const ticketText = generateTicketText(posCart, total);
                downloadTicket(ticketText);

                showToast("Cobro exitoso. Stock en base de datos actualizado.");
                posCart = []; 
                
                updatePOSCartUI();
                await fetchProducts(); 

                document.getElementById('pos-search').value = "";
                filterPOSProducts();
            } catch (error) {
                console.error(error);
                alert("Hubo un error contactando la base de datos. Verifica tu conexion.");
            } finally {
                btnCobrar.innerHTML = '<i class="fa-solid fa-print"></i> Cobrar e Imprimir';
                btnCobrar.disabled = false;
            }
        }

        // =========================================================================
        // INICIO AUTOMATICO
        // =========================================================================
        
        // Funcion: Ejecuta la carga de datos al momento exacto que abres la aplicacion
        window.onload = () => {
            fetchProducts();
            
            // Verificacion de seguridad: Mantiene al usuario en la caja si recarga la pagina sin cerrar sesion
            if(localStorage.getItem('pos_logged_in') === 'true') {
                switchView('pos');
            } else {
                switchView('store');
            }
        };
    </script>
</body>
</html>
