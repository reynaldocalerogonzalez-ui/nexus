<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS | Directorio de Servicios Profesionales</title>
    
    <meta name="description" content="NEXUS conecta a los mejores profesionales de servicios con clientes locales. Plomería, Roofing, Limpieza y más.">
    <meta name="keywords" content="servicios, plomero, carpintero, limpieza, nexus, negocio local">
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700;900&display=swap');
        body { font-family: 'Inter', sans-serif; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(10px); }
        .featured-card { border: 2px solid #3b82f6; position: relative; }
        .featured-card::after { content: 'DESTACADO'; position: absolute; top: -10px; right: 10px; background: #3b82f6; color: white; font-size: 10px; padding: 2px 8px; border-radius: 4px; font-weight: bold; }
    </style>
</head>
<body class="bg-gray-50 text-gray-900">

    <nav class="sticky top-0 z-50 glass border-b border-gray-200">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="text-2xl font-black tracking-tighter text-slate-900">NEX<span class="text-blue-600">US</span></div>
            <a href="#unirse" class="hidden md:block bg-blue-600 text-white px-5 py-2 rounded-full text-sm font-bold hover:bg-blue-700 transition">Anuncia tu Negocio</a>
        </div>
    </nav>

    <header class="bg-slate-900 pt-20 pb-32 px-6">
        <div class="container mx-auto text-center">
            <h1 class="text-4xl md:text-6xl font-black text-white mb-6 tracking-tight">
                Encuentra expertos en <span class="text-blue-500">segundos.</span>
            </h1>
            <p class="text-gray-400 text-lg mb-10 max-w-2xl mx-auto">La infraestructura que conecta el talento local con la necesidad inmediata.</p>
            
            <div class="max-w-3xl mx-auto flex flex-col md:flex-row shadow-2xl rounded-2xl overflow-hidden bg-white p-2">
                <input type="text" id="mainSearch" onkeyup="filterServices()" placeholder="¿Qué servicio necesitas? (Ej: Plomero, Roof...)" class="w-full p-4 text-gray-700 focus:outline-none text-lg">
                <button class="bg-blue-600 text-white px-10 py-4 font-bold hover:bg-blue-700 transition uppercase tracking-widest">Buscar</button>
            </div>
        </div>
    </header>

    <section class="container mx-auto -mt-12 px-6">
        <div class="flex overflow-x-auto pb-4 gap-4 no-scrollbar justify-start md:justify-center">
            <button onclick="filterByCategory('Todos')" class="cat-btn bg-white shadow-md px-6 py-3 rounded-xl font-bold hover:bg-blue-50 transition border border-gray-100 whitespace-nowrap">Todos</button>
            <button onclick="filterByCategory('Plomería')" class="cat-btn bg-white shadow-md px-6 py-3 rounded-xl font-bold hover:bg-blue-50 transition border border-gray-100 whitespace-nowrap">Plomería</button>
            <button onclick="filterByCategory('Roofing')" class="cat-btn bg-white shadow-md px-6 py-3 rounded-xl font-bold hover:bg-blue-50 transition border border-gray-100 whitespace-nowrap">Roofing</button>
            <button onclick="filterByCategory('Limpieza')" class="cat-btn bg-white shadow-md px-6 py-3 rounded-xl font-bold hover:bg-blue-50 transition border border-gray-100 whitespace-nowrap">Limpieza</button>
            <button onclick="filterByCategory('Basura')" class="cat-btn bg-white shadow-md px-6 py-3 rounded-xl font-bold hover:bg-blue-50 transition border border-gray-100 whitespace-nowrap">Basura/Chatarra</button>
        </div>
    </section>

    <main class="container mx-auto py-20 px-6">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8" id="businessGrid">
            </div>
    </main>

    <footer class="bg-white border-t border-gray-200 py-20" id="unirse">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-3xl font-bold mb-4 text-slate-900">¿Tienes un negocio?</h2>
            <p class="text-gray-600 mb-8 max-w-xl mx-auto">Únete a la red NEXUS y empieza a recibir clientes verificados directamente a tu WhatsApp.</p>
           <a href="https://wa.me/17863239057?text=Hola%20Rey,%20me%20interesa%20unirme%20a%20NEXUS.%20¿Podrías%20darme%20detalles%20para%20anunciar%20mi%20negocio?" class="inline-block bg-slate-900 text-white px-10 py-4 rounded-full font-black hover:bg-blue-600 transition shadow-xl text-center">EMPEZAR GRATIS HOY</a>    </div>
 </footer>
    <script>
        // BASE DE DATOS - Aquí es donde agregarás los futuros negocios
        const businesses = [
            {
                name: "Plomería El Rayo",
                category: "Plomería",
                desc: "Atención de emergencias 24/7. Fugas, drenajes y calentadores.",
                city: "Miami, FL",
                rating: 5,
                whatsapp: "123456789",
                featured: true
            },
            {
                name: "Roofing Master",
                category: "Roofing",
                desc: "Expertos en techos, reparación de tejas y goteras. Presupuesto gratis.",
                city: "Doral, FL",
                rating: 4,
                whatsapp: "987654321",
                featured: false
            },
            {
                name: "Eco-Chatarra Rey",
                category: "Basura",
                desc: "Recolección de escombros, metales y basura pesada. Limpieza total.",
                city: "Hialeah, FL",
                rating: 5,
                whatsapp: "112233445",
                featured: true
            }
        ];

        function renderBusinesses(data) {
            const grid = document.getElementById('businessGrid');
            grid.innerHTML = '';
            
            data.forEach(biz => {
                const card = document.createElement('div');
                card.className = `bg-white rounded-3xl p-8 shadow-sm border border-gray-100 hover:shadow-2xl transition-all duration-300 ${biz.featured ? 'featured-card' : ''}`;
                
                let stars = '⭐'.repeat(biz.rating);
                
                card.innerHTML = `
                    <div class="flex justify-between items-start mb-6">
                        <span class="text-[10px] font-black uppercase tracking-widest text-blue-600 bg-blue-50 px-3 py-1 rounded-full border border-blue-100">${biz.category}</span>
                        <span class="text-sm font-bold text-gray-400">${stars}</span>
                    </div>
                    <h3 class="text-2xl font-black text-slate-900 mb-3">${biz.name}</h3>
                    <p class="text-gray-500 text-sm leading-relaxed mb-6">${biz.desc}</p>
                    <div class="flex items-center text-gray-400 text-xs mb-8">
                        <i class="fas fa-map-marker-alt mr-2 text-blue-500"></i> ${biz.city}
                    </div>
                    <a href="https://wa.me/${biz.whatsapp}" target="_blank" class="block w-full text-center bg-slate-900 text-white py-4 rounded-2xl font-bold hover:bg-blue-600 transition shadow-lg">
                        <i class="fab fa-whatsapp mr-2"></i> CONTACTAR
                    </a>
                `;
                grid.appendChild(card);
            });
        }

        // Buscador en tiempo real
        function filterServices() {
            const query = document.getElementById('mainSearch').value.toLowerCase();
            const filtered = businesses.filter(b => 
                b.name.toLowerCase().includes(query) || 
                b.category.toLowerCase().includes(query) ||
                b.desc.toLowerCase().includes(query)
            );
            renderBusinesses(filtered);
        }

        // Filtro por categoría
        function filterByCategory(cat) {
            if(cat === 'Todos') {
                renderBusinesses(businesses);
            } else {
                const filtered = businesses.filter(b => b.category === cat);
                renderBusinesses(filtered);
            }
        }

        // Carga inicial
        renderBusinesses(businesses);
    </script>
</body>
</html>
