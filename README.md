import React, { useMemo, useState } from "react"; import { motion, AnimatePresence } from "framer-motion"; import { Search, Star, ShoppingCart, LogIn, ChevronRight, X, Tag, Filter, Globe2, MapPin, Wallet, ShieldCheck, Clock, CheckCircle2 } from "lucide-react";

// ===================================================== // VINTENA — MVP FRONTEND (SPA) // - React + TailwindCSS (sem dependências estranhas) // - UX moderna, focada em mobile-first // - Componentes acessíveis e reutilizáveis // - Dados mockados para demonstração (substituir por API) // =====================================================

// Paleta (vibe nova, diferente do site referenciado): // Primária: roxo #6D28D9  → tailwind: purple-700 // Destaque: ciano #06B6D4 → tailwind: cyan-500 // Neutros: slate / zinc

const CATEGORIES = [ { id: "design", name: "Design & Criativo", emoji: "🎨" }, { id: "marketing", name: "Marketing Digital", emoji: "📣" }, { id: "escrita", name: "Escrita & Tradução", emoji: "✍️" }, { id: "video", name: "Vídeo & Animação", emoji: "🎬" }, { id: "web", name: "Web & Tecnologia", emoji: "💻" }, { id: "negocios", name: "Negócios & Consultoria", emoji: "🧠" }, ];

const SERVICES = [ { id: "srv-1", title: "Logo minimalista profissional", seller: "Ana Ribeiro", rating: 4.9, reviews: 182, price: 20, thumb: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b?q=80&w=1000&auto=format&fit=crop", category: "design", extras: [ { id: "ex-1", name: "Entrega 24h", price: 15 }, { id: "ex-2", name: "Manual de marca (PDF)", price: 30 }, ], description: "Crio um logotipo minimalista, versátil e memorável. Entrego arquivos em PNG/SVG e preview aplicado.", tags: ["logo", "branding", "minimalista"], }, { id: "srv-2", title: "Edição de vídeo para Reels (até 40s)", seller: "Bruno Martins", rating: 4.8, reviews: 96, price: 20, thumb: "https://images.unsplash.com/photo-1526948128573-703ee1aeb6fa?q=80&w=1180&auto=format&fit=crop", category: "video", extras: [ { id: "ex-3", name: "Legenda automática", price: 10 }, { id: "ex-4", name: "Capas animadas", price: 20 }, ], description: "Cortes dinâmicos, transições suaves e otimização para engajamento no Instagram e TikTok.", tags: ["reels", "shorts", "tiktok"], }, { id: "srv-3", title: "Landing page responsiva (1 seção)", seller: "Carla Souza", rating: 4.7, reviews: 64, price: 20, thumb: "https://images.unsplash.com/photo-1508830524289-0adcbe822b40?q=80&w=1180&auto=format&fit=crop", category: "web", extras: [ { id: "ex-5", name: "Formulário + lead", price: 20 }, { id: "ex-6", name: "Hospedagem e domínio", price: 60 }, ], description: "Landing moderna com Tailwind, SEO básico e performance otimizada.", tags: ["landing", "tailwind", "seo"], }, { id: "srv-4", title: "Gestão de tráfego (setup inicial)", seller: "Diego Lima", rating: 4.6, reviews: 71, price: 20, thumb: "https://images.unsplash.com/photo-1498050108023-c5249f4df085?q=80&w=1180&auto=format&fit=crop", category: "marketing", extras: [ { id: "ex-7", name: "Pixel + eventos", price: 25 }, { id: "ex-8", name: "Relatório 30 dias", price: 40 }, ], description: "Criação de campanhas, públicos e instalação de pixel para começar a rodar com estratégia.", tags: ["meta ads", "google ads", "pixel"], }, { id: "srv-5", title: "Tradução PT ↔️ ES (até 300 palavras)", seller: "Esteban Duarte", rating: 5.0, reviews: 41, price: 20, thumb: "https://images.unsplash.com/photo-1554224155-6726b3ff858f?q=80&w=1180&auto=format&fit=crop", category: "escrita", extras: [ { id: "ex-9", name: "Entrega 12h", price: 20 }, { id: "ex-10", name: "Revisão dupla", price: 10 }, ], description: "Tradução humana, contextual e com revisão. Entrego em DOCX/PDF.", tags: ["espanhol", "tradução", "pt-br"], }, { id: "srv-6", title: "Mentoria express (30 min) para MEI", seller: "Marina Campos", rating: 4.9, reviews: 23, price: 20, thumb: "https://images.unsplash.com/photo-1542744094-24638eff58bb?q=80&w=1180&auto=format&fit=crop", category: "negocios", extras: [ { id: "ex-11", name: "Plano de ação (PDF)", price: 25 }, ], description: "Tira-dúvidas sobre precificação, proposta e fluxo do MEI com ações práticas.", tags: ["mentoria", "mei", "negócios"], }, ];

function cx(...classes) { return classes.filter(Boolean).join(" "); }

function Header({ onOpenAuth, cartCount }) { return ( <header className="sticky top-0 z-40 backdrop-blur supports-[backdrop-filter]:bg-white/70 bg-white/80 border-b border-slate-200"> <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between"> <div className="flex items-center gap-3"> <div className="h-9 w-9 rounded-2xl bg-gradient-to-br from-purple-700 to-cyan-500 grid place-items-center text-white font-bold">V</div> <div className="leading-tight"> <div className="text-lg font-extrabold tracking-tight text-slate-900">Vintena</div> <div className="text-xs text-slate-500 -mt-0.5">Serviços a partir de R$ 20</div> </div> </div>

<div className="hidden md:flex items-center gap-2 flex-1 max-w-xl mx-6">
      <div className="relative flex-1">
        <Search className="absolute left-3 top-1/2 -translate-y-1/2 h-5 w-5 text-slate-400" />
        <input
          placeholder="Buscar serviços, ex: logo, tráfego, site..."
          className="w-full pl-10 pr-4 py-2 rounded-xl border border-slate-200 focus:outline-none focus:ring-4 focus:ring-purple-100 focus:border-purple-400"
        />
      </div>
      <button className="px-3 py-2 rounded-xl border border-slate-200 hover:bg-slate-50 text-sm flex items-center gap-2"><Filter className="h-4 w-4"/>Filtros</button>
    </div>

    <div className="flex items-center gap-2">
      <button onClick={onOpenAuth} className="hidden sm:inline-flex items-center gap-2 px-3 py-2 text-sm rounded-xl border border-slate-200 hover:bg-slate-50"><LogIn className="h-4 w-4"/> Entrar</button>
      <button className="relative p-2 rounded-xl border border-slate-200 hover:bg-slate-50">
        <ShoppingCart className="h-5 w-5"/>
        {cartCount > 0 && (
          <span className="absolute -top-1 -right-1 text-[10px] bg-purple-700 text-white rounded-full px-1.5 py-0.5">{cartCount}</span>
        )}
      </button>
    </div>
  </div>
</header>

); }

function Hero() { return ( <section className="bg-gradient-to-br from-purple-50 via-white to-cyan-50"> <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16"> <div className="grid md:grid-cols-2 items-center gap-8"> <div> <motion.h1 initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.5 }} className="text-3xl md:text-5xl font-extrabold tracking-tight text-slate-900"> Encontre talentos brasileiros por <span className="bg-gradient-to-r from-purple-700 to-cyan-500 bg-clip-text text-transparent">R$20</span> </motion.h1> <p className="mt-4 text-slate-600 max-w-prose"> A Vintena conecta você a especialistas de verdade, com entrega ágil, proteção ao comprador e avaliação transparente. </p> <div className="mt-6 flex flex-wrap gap-3"> <a href="#categorias" className="px-4 py-2 rounded-2xl bg-slate-900 text-white hover:opacity-90">Explorar categorias</a> <a href="#como-funciona" className="px-4 py-2 rounded-2xl border border-slate-300 hover:bg-white">Como funciona</a> </div> <div className="mt-6 flex items-center gap-4 text-sm text-slate-600"> <div className="flex items-center gap-1"><ShieldCheck className="h-4 w-4"/> Compra garantida</div> <div className="flex items-center gap-1"><Clock className="h-4 w-4"/> Entrega no prazo</div> <div className="flex items-center gap-1"><Globe2 className="h-4 w-4"/> PIX e cartão</div> </div> </div> <motion.div initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.6 }} className="relative"> <div className="aspect-[4/3] rounded-3xl overflow-hidden shadow-xl ring-1 ring-black/5"> <img alt="Talentos trabalhando" className="object-cover w-full h-full" src="https://images.unsplash.com/photo-1521737604893-d14cc237f11d?q=80&w=1600&auto=format&fit=crop"/> </div> <div className="absolute -bottom-4 -left-4 bg-white rounded-2xl shadow-lg p-3 border border-slate-200 flex items-center gap-2"> <Tag className="h-4 w-4 text-purple-700"/> <div className="text-sm"><span className="font-semibold">Serviços a partir de R$20</span> — sem letra miúda</div> </div> </motion.div> </div> </div> </section> ); }

function CategoryPills({ active, onChange }) { return ( <div id="categorias" className="flex gap-2 overflow-auto no-scrollbar py-2"> {CATEGORIES.map((c) => ( <button key={c.id} onClick={() => onChange(c.id === active ? undefined : c.id)} className={cx( "px-3 py-1.5 rounded-full border text-sm whitespace-nowrap", active === c.id ? "bg-purple-700 border-purple-700 text-white" : "border-slate-300 hover:bg-slate-50" )} aria-pressed={active === c.id} > <span className="mr-1.5">{c.emoji}</span> {c.name} </button> ))} </div> ); }

function ServiceCard({ service, onOpen }) { return ( <motion.button layout onClick={() => onOpen(service)} className="group text-left bg-white rounded-2xl border border-slate-200 hover:border-purple-200 hover:shadow-md transition p-3"> <div className="aspect-[16/10] rounded-xl overflow-hidden bg-slate-100"> <img src={service.thumb} alt="thumb" className="w-full h-full object-cover group-hover:scale-[1.02] transition"/> </div> <div className="mt-3 flex items-start justify-between gap-2"> <div> <h3 className="font-semibold text-slate-900 line-clamp-2">{service.title}</h3> <div className="mt-1 text-sm text-slate-600">por {service.seller}</div> <div className="mt-1 flex items-center gap-1 text-sm text-slate-700"> <Star className="h-4 w-4 fill-yellow-400 stroke-yellow-400"/> {service.rating} <span className="text-slate-400">•</span> <span>{service.reviews} avaliações</span> </div> </div> <div className="text-right"> <div className="text-xs text-slate-500">a partir de</div> <div className="text-lg font-extrabold text-slate-900">R$ {service.price.toFixed(2)}</div> </div> </div> <div className="mt-2 flex flex-wrap gap-1"> {service.tags.map((t) => ( <span key={t} className="text-xs px-2 py-1 rounded-full bg-slate-100 text-slate-600">#{t}</span> ))} </div> </motion.button> ); }

function ServiceModal({ open, onClose, service, onAddToCart }) { if (!service) return null; return ( <AnimatePresence> {open && ( <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }} className="fixed inset-0 z-50 bg-black/40"> <motion.div initial={{ y: 24, opacity: 0 }} animate={{ y: 0, opacity: 1 }} exit={{ y: 24, opacity: 0 }} className="absolute inset-x-3 md:inset-x-auto md:right-8 top-8 md:max-w-xl bg-white rounded-3xl shadow-2xl border border-slate-200"> <div className="p-4 border-b flex items-center justify-between"> <div className="font-semibold">Detalhes do serviço</div> <button onClick={onClose} className="p-2 rounded-xl hover:bg-slate-50"><X className="h-5 w-5"/></button> </div> <div className="p-4 grid gap-4"> <div className="aspect-[16/9] overflow-hidden rounded-2xl bg-slate-100"> <img src={service.thumb} alt="thumb" className="w-full h-full object-cover"/> </div> <div> <h3 className="text-xl font-extrabold text-slate-900">{service.title}</h3> <div className="mt-1 text-slate-600">por {service.seller}</div> <p className="mt-3 text-slate-700 leading-relaxed">{service.description}</p> </div> <div className="grid gap-2"> <div className="font-semibold">Extras</div> <div className="grid gap-2"> {service.extras.map((ex) => ( <label key={ex.id} className="flex items-center justify-between p-3 rounded-xl border border-slate-200"> <span>{ex.name}</span> <span className="font-semibold">+ R$ {ex.price.toFixed(2)}</span> </label> ))} </div> </div> <button onClick={() => onAddToCart(service)} className="w-full inline-flex items-center justify-center gap-2 px-4 py-3 rounded-2xl bg-gradient-to-r from-purple-700 to-cyan-500 text-white font-semibold shadow hover:opacity-95"> <ShoppingCart className="h-5 w-5"/> Adicionar ao carrinho — R$ {service.price.toFixed(2)} </button> </div> </motion.div> </motion.div> )} </AnimatePresence> ); }

function Feature({ icon: Icon, title, desc }) { return ( <div className="p-4 rounded-2xl border border-slate-200 bg-white"> <div className="flex items-center gap-2 text-slate-900 font-semibold"><Icon className="h-5 w-5"/> {title}</div> <p className="mt-1 text-slate-600 text-sm">{desc}</p> </div> ); }

function Footer() { return ( <footer className="border-t mt-16"> <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 grid md:grid-cols-4 gap-8 text-sm"> <div> <div className="flex items-center gap-2"> <div className="h-9 w-9 rounded-2xl bg-gradient-to-br from-purple-700 to-cyan-500 grid place-items-center text-white font-bold">V</div> <div className="text-lg font-extrabold text-slate-900">Vintena</div> </div> <p className="mt-3 text-slate-600">Marketplace brasileiro de serviços rápidos, com proteção ao comprador e pagamentos via PIX e cartão.</p> </div> <div> <div className="font-semibold text-slate-900">Categorias</div> <ul className="mt-2 space-y-1 text-slate-600"> {CATEGORIES.map(c => <li key={c.id}>{c.name}</li>)} </ul> </div> <div> <div className="font-semibold text-slate-900">Institucional</div> <ul className="mt-2 space-y-1 text-slate-600"> <li>Sobre</li> <li>Termos de uso</li> <li>Política de privacidade</li> <li>Contato</li> </ul> </div> <div> <div className="font-semibold text-slate-900">Pagamento</div> <ul className="mt-2 space-y-1 text-slate-600"> <li>PIX</li> <li>Cartão de crédito</li> <li>Boleto</li> </ul> </div> </div> <div className="py-4 text-center text-xs text-slate-500">© {new Date().getFullYear()} Vintena — Todos os direitos reservados.</div> </footer> ); }

export default function App() { const [activeCategory, setActiveCategory] = useState(); const [query, setQuery] = useState(""); const [authOpen, setAuthOpen] = useState(false); const [modalOpen, setModalOpen] = useState(false); const [selected, setSelected] = useState(null); const [cart, setCart] = useState([]);

const filtered = useMemo(() => { return SERVICES.filter((s) => (!activeCategory || s.category === activeCategory) && (query.trim().length === 0 || [s.title, s.description, s.tags.join(" "), s.seller] .join(" ") .toLowerCase() .includes(query.toLowerCase())) ); }, [activeCategory, query]);

const openService = (s) => { setSelected(s); setModalOpen(true); };

const addToCart = (s) => { setCart((prev) => [...prev, { id: s.id, title: s.title, price: s.price }]); setModalOpen(false); };

return ( <div className="min-h-screen bg-slate-50"> <Header onOpenAuth={() => setAuthOpen(true)} cartCount={cart.length} /> <main> <Hero />

<section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 -mt-8">
      <div className="bg-white rounded-3xl border border-slate-200 p-4 md:p-6 shadow-sm">
        {/* Busca (mobile-first) */}
        <div className="md:hidden mb-3">
          <div className="relative">
            <Search className="absolute left-3 top-1/2 -translate-y-1/2 h-5 w-5 text-slate-400" />
            <input
              value={query}
              onChange={(e) => setQuery(e.target.value)}
              placeholder="Buscar serviços..."
              className="w-full pl-10 pr-4 py-2 rounded-xl border border-slate-200 focus:outline-none focus:ring-4 focus:ring-purple-100 focus:border-purple-400"
            />
          </div>
        </div>

        <CategoryPills active={activeCategory} onChange={setActiveCategory} />

        {/* Grid de serviços */}
        <div className="mt-4 grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
          <AnimatePresence mode="popLayout">
            {filtered.map((s) => (
              <ServiceCard key={s.id} service={s} onOpen={openService} />
            ))}
          </AnimatePresence>
        </div>

        {filtered.length === 0 && (
          <div className="text-center py-12 text-slate-600">
            Nenhum serviço encontrado para sua busca.
          </div>
        )}
      </div>
    </section>

    {/* Seção Como funciona */}
    <section id="como-funciona" className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-12">
      <h2 className="text-2xl font-extrabold text-slate-900">Como funciona</h2>
      <p className="text-slate-600 mt-1">Simples, transparente e seguro para compradores e vendedores.</p>
      <div className="mt-4 grid md:grid-cols-3 gap-4">
        <Feature icon={Search} title="1. Encontre" desc="Busque por categoria e compare avaliações reais." />
        <Feature icon={Wallet} title="2. Pague" desc="Pague via PIX/cartão. O valor fica em custódia até a entrega." />
        <Feature icon={CheckCircle2} title="3. Receba" desc="Aprovar, revisar e baixar os arquivos pelo painel." />
      </div>
    </section>

    {/* CTA vendedores */}
    <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-12">
      <div className="bg-gradient-to-r from-purple-700 to-cyan-500 rounded-3xl p-6 md:p-10 text-white relative overflow-hidden">
        <div className="absolute inset-0 opacity-10" style={{backgroundImage: "radial-gradient(circle at 20% 20%, white 2px, transparent 2px)"}}/>
        <h3 className="text-2xl md:text-3xl font-extrabold">Venda seus serviços na Vintena</h3>
        <p className="mt-2 text-white/80 max-w-prose">Publique em minutos, defina extras e prazos, receba por PIX. Proteção contra calote e painel de pedidos claro.</p>
        <a href="#" className="mt-4 inline-flex items-center gap-2 px-4 py-2 rounded-2xl bg-white text-slate-900 font-semibold shadow">
          Começar agora <ChevronRight className="h-4 w-4"/>
        </a>
      </div>
    </section>

    <Footer />
  </main>

  {/* MODAL: Login simples (mock) */}
  <AnimatePresence>
    {authOpen && (
      <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }} className="fixed inset-0 z-50 bg-black/40">
        <motion.div initial={{ y: 24, opacity: 0 }} animate={{ y: 0, opacity: 1 }} exit={{ y: 24, opacity: 0 }} className="absolute inset-x-3 md:inset-x-auto md:right-8 top-8 md:max-w-md bg-white rounded-3xl shadow-2xl border border-slate-200">
          <div className="p-4 border-b flex items-center justify-between">
            <div className="font-semibold">Acessar sua conta</div>
            <button onClick={() => setAuthOpen(false)} className="p-2 rounded-xl hover:bg-slate-50"><X className="h-5 w-5"/></button>
          </div>
          <div className="p-4 grid gap-3">
            <label className="grid gap-1 text-sm">
              <span>Email</span>
              <input className="px-3 py-2 rounded-xl border border-slate-200" placeholder="voce@email.com"/>
            </label>
            <label className="grid gap-1 text-sm">
              <span>Senha</span>
              <input type="password" className="px-3 py-2 rounded-xl border border-slate-200" placeholder="••••••••"/>
            </label>
            <button className="mt-2 inline-flex items-center justify-center gap-2 px-4 py-2 rounded-2xl bg-slate-900 text-white font-semibold hover:opacity-90">Entrar</button>
            <div className="text-xs text-slate-500 text-center">Ao continuar, você concorda com os Termos e a Política de Privacidade.</div>
          </div>
        </motion.div>
      </motion.div>
    )}
  </AnimatePresence>

  {/* MODAL: Serviço */}
  <ServiceModal open={modalOpen} onClose={() => setModalOpen(false)} service={selected} onAddToCart={addToCart} />
</div>

); }

// ============================= // DICAS DE INTEGRAÇÃO (BACKEND) // - Autenticação: Supabase/Auth.js // - Banco: Postgres (Pedidos, Serviços, Usuários, Avaliações, Pagamentos) // - Pagamentos: Stripe + PIX (via PSP parceiro) // - Upload: S3/Cloudflare R2 // - SEO/SSR: Next.js 14 (este arquivo vira uma página/rota) // - Anti-fraude: liberação escalonada e verificação de identidade para vendedores // =============================

# Site
