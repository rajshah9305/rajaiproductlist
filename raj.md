import React, { useState, useMemo } from 'react';
import { Search, ShoppingCart, User, TrendingUp, Star, Download, DollarSign, Github, ExternalLink, X, Check, Sparkles, Zap, Shield, Award } from 'lucide-react';

const DigitalMarketplace = () => {
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedCategory, setSelectedCategory] = useState('All');
  const [cart, setCart] = useState([]);
  const [showCart, setShowCart] = useState(false);
  const [notification, setNotification] = useState('');
  const [hoveredProduct, setHoveredProduct] = useState(null);

  const products = [
    {
      id: 1,
      title: "No-Code AI App Builder with Gemini API",
      repoName: "nocodeaigeminiapi",
      category: "AI Tools",
      price: 149,
      rating: 4.9,
      sales: 234,
      image: "https://images.unsplash.com/photo-1677442136019-21780ecad995?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Build powerful AI applications without writing code using Google’s Gemini API. Complete TypeScript implementation.",
      tags: ["Gemini", "No-Code", "TypeScript", "AI"],
      githubUrl: "https://github.com/rajshah9305/nocodeaigeminiapi",
      features: ["Drag & Drop Interface", "Gemini API Integration", "Export to Code", "Template Library"]
    },
    {
      id: 2,
      title: "AI Agent Orchestration Platform",
      repoName: "AIAgentOrchestrationPlatform",
      category: "AI Tools",
      price: 199,
      rating: 5.0,
      sales: 156,
      image: "https://images.unsplash.com/photo-1620712943543-bcc4688e7485?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Ultra-fast AI agent management with Cerebras integration. MIT Licensed. Perfect for building complex AI workflows.",
      tags: ["Cerebras", "AI Agents", "TypeScript", "Orchestration"],
      githubUrl: "https://github.com/rajshah9305/AIAgentOrchestrationPlatform",
      featured: true,
      features: ["Multi-Agent Support", "Cerebras Ultra-Fast", "Workflow Builder", "Real-time Monitoring"]
    },
    {
      id: 3,
      title: "AWS Bedrock Agent Builder",
      repoName: "bedrock-agent-builder",
      category: "Cloud Tools",
      price: 129,
      rating: 4.8,
      sales: 189,
      image: "https://images.unsplash.com/photo-1451187580459-43490279c0fa?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Complete toolkit for building AI agents on AWS Bedrock. Includes live demo deployment.",
      tags: ["AWS", "Bedrock", "AI Agents", "JavaScript"],
      githubUrl: "https://github.com/rajshah9305/bedrock-agent-builder",
      demoUrl: "https://quiet-pika-b180fc.netlify.app/",
      features: ["AWS Integration", "Agent Templates", "Live Dashboard", "Deployment Ready"]
    },
    {
      id: 4,
      title: "RAJ AI App Builder",
      repoName: "RAJaiappbuilder",
      category: "AI Tools",
      price: 179,
      rating: 4.9,
      sales: 167,
      image: "https://images.unsplash.com/photo-1555949963-ff9fe0c870eb?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Professional AI application builder with MIT license. TypeScript-based with modern UI/UX.",
      tags: ["TypeScript", "AI Builder", "MIT License", "Modern UI"],
      githubUrl: "https://github.com/rajshah9305/RAJaiappbuilder",
      features: ["Visual Builder", "Component Library", "Export Options", "MIT Licensed"]
    },
    {
      id: 5,
      title: "Coding Nexus AI",
      repoName: "codingnexusai",
      category: "Developer Tools",
      price: 99,
      rating: 4.7,
      sales: 312,
      image: "https://images.unsplash.com/photo-1542831371-29b0f74f9713?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "AI-powered coding assistant with MIT license. Boost your development productivity instantly.",
      tags: ["JavaScript", "Coding AI", "Developer Tools", "MIT"],
      githubUrl: "https://github.com/rajshah9305/codingnexusai",
      features: ["Code Generation", "Bug Detection", "Refactoring Tools", "Multi-Language"]
    },
    {
      id: 6,
      title: "AWS Chat Application",
      repoName: "chatawsapp",
      category: "Cloud Tools",
      price: 89,
      rating: 4.6,
      sales: 278,
      image: "https://images.unsplash.com/photo-1587825140708-dfaf72ae4b04?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Full-featured chat application built on AWS infrastructure with TypeScript.",
      tags: ["AWS", "Chat", "TypeScript", "Real-time"],
      githubUrl: "https://github.com/rajshah9305/chatawsapp",
      demoUrl: "https://awsapp-pied.vercel.app/",
      features: ["Real-time Messaging", "AWS Backend", "Scalable Architecture", "Live Demo"]
    },
    {
      id: 7,
      title: "CrewAI with Cerebras Integration",
      repoName: "crewsaicerebras",
      category: "AI Tools",
      price: 159,
      rating: 4.8,
      sales: 145,
      image: "https://images.unsplash.com/photo-1635070041078-e363dbe005cb?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Multi-agent AI system using CrewAI framework with ultra-fast Cerebras inference.",
      tags: ["Python", "CrewAI", "Cerebras", "Multi-Agent"],
      githubUrl: "https://github.com/rajshah9305/crewsaicerebras",
      features: ["CrewAI Framework", "Cerebras Speed", "Multi-Agent Workflows", "Python-Based"]
    },
    {
      id: 8,
      title: "NLP with Cerebras",
      repoName: "NLPCEREBRAS",
      category: "AI Tools",
      price: 139,
      rating: 4.7,
      sales: 198,
      image: "https://images.unsplash.com/photo-1516110833967-0b5716ca1387?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Natural Language Processing toolkit powered by Cerebras for lightning-fast inference.",
      tags: ["NLP", "Cerebras", "TypeScript", "AI"],
      githubUrl: "https://github.com/rajshah9305/NLPCEREBRAS",
      features: ["Fast Inference", "NLP Models", "Easy Integration", "Production Ready"]
    },
    {
      id: 9,
      title: "Magnet Masterpiece Studio",
      repoName: "magnet-masterpiece-studio",
      category: "Creative Tools",
      price: 79,
      rating: 4.9,
      sales: 456,
      image: "https://images.unsplash.com/photo-1561070791-2526d30994b5?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Creative design studio for building custom magnet designs. TypeScript with modern UI.",
      tags: ["Design", "TypeScript", "Creative", "Studio"],
      githubUrl: "https://github.com/rajshah9305/magnet-masterpiece-studio",
      features: ["Design Tools", "Export Options", "Template Gallery", "Easy to Use"]
    },
    {
      id: 10,
      title: "YYC Fridge Magnets Platform",
      repoName: "yycfridgemagnets",
      category: "Creative Tools",
      price: 59,
      rating: 4.5,
      sales: 523,
      image: "https://images.unsplash.com/photo-1513542789411-b6a5d4f31634?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Complete platform for creating and selling custom fridge magnets. JavaScript-based.",
      tags: ["JavaScript", "E-commerce", "Design", "Creative"],
      githubUrl: "https://github.com/rajshah9305/yycfridgemagnets",
      features: ["Custom Designs", "E-commerce Ready", "Order Management", "Print Integration"]
    },
    {
      id: 11,
      title: "AWS Bedrock Development Kit",
      repoName: "AWSBEDROCK",
      category: "Cloud Tools",
      price: 169,
      rating: 4.8,
      sales: 134,
      image: "https://images.unsplash.com/photo-1667372393119-3d4c48d07fc9?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Complete development kit for AWS Bedrock with MIT license. TypeScript implementation.",
      tags: ["AWS", "Bedrock", "TypeScript", "MIT License"],
      githubUrl: "https://github.com/rajshah9305/AWSBEDROCK",
      features: ["Full AWS Integration", "TypeScript", "MIT Licensed", "Documentation"]
    },
    {
      id: 12,
      title: "Fantasy Gallery Platform",
      repoName: "fantasygallery",
      category: "Creative Tools",
      price: 119,
      rating: 4.6,
      sales: 201,
      image: "https://images.unsplash.com/photo-1561214115-f2f134cc4912?w=400&h=300&fit=crop",
      author: "Raj Shah",
      description: "Beautiful gallery platform for showcasing creative work. Built with TypeScript.",
      tags: ["Gallery", "TypeScript", "Portfolio", "Creative"],
      githubUrl: "https://github.com/rajshah9305/fantasygallery",
      features: ["Responsive Gallery", "Modern UI", "Portfolio Ready", "Easy Setup"]
    }
  ];

  const categories = ['All', 'AI Tools', 'Cloud Tools', 'Developer Tools', 'Creative Tools'];

  const filteredProducts = useMemo(() => {
    return products.filter(product => {
      const matchesSearch = product.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
        product.tags.some(tag => tag.toLowerCase().includes(searchQuery.toLowerCase())) ||
        product.description.toLowerCase().includes(searchQuery.toLowerCase());
      const matchesCategory = selectedCategory === 'All' || product.category === selectedCategory;
      return matchesSearch && matchesCategory;
    });
  }, [searchQuery, selectedCategory, products]);

  const addToCart = (product) => {
    setCart([...cart, product]);
    setNotification(`${product.title} added to cart!`);
    setTimeout(() => setNotification(''), 3000);
  };

  const removeFromCart = (productId) => {
    // Find the index of the first item with this product ID
    const indexToRemove = cart.findIndex(item => item.id === productId);
    
    // If found, remove it
    if (indexToRemove > -1) {
      const newCart = [...cart];
      newCart.splice(indexToRemove, 1);
      setCart(newCart);
    }
  };

  const cartTotal = cart.reduce((sum, item) => sum + item.price, 0);
  const totalRevenue = products.reduce((sum, p) => sum + (p.price * p.sales), 0);
  const totalSales = products.reduce((sum, p) => sum + p.sales, 0);

  return (
    <div className="min-h-screen bg-gradient-to-br from-emerald-50 via-teal-50 to-cyan-50 font-sans">
      {/* Notification Toast */}
      {notification && (
        <div className="fixed top-20 right-4 z-50 bg-gradient-to-r from-emerald-500 to-teal-500 text-white px-6 py-3 rounded-xl shadow-2xl flex items-center gap-3 transition-all duration-300">
          <Check className="w-5 h-5" />
          <span className="font-medium">{notification}</span>
        </div>
      )}

      {/* Header */}
      <header className="bg-white/80 backdrop-blur-xl border-b border-emerald-100 sticky top-0 z-40 shadow-lg">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex items-center justify-between h-16">
            <div className="flex items-center space-x-3">
              <div className="relative">
                <div className="w-12 h-12 bg-gradient-to-br from-emerald-500 via-teal-500 to-cyan-500 rounded-2xl flex items-center justify-center transform rotate-3 hover:rotate-0 transition-transform duration-300">
                  <Sparkles className="w-6 h-6 text-white" />
                </div>
                <div className="absolute -top-1 -right-1 w-3 h-3 bg-yellow-400 rounded-full animate-pulse"></div>
              </div>
              <div>
                <span className="text-2xl font-black bg-gradient-to-r from-emerald-600 via-teal-600 to-cyan-600 bg-clip-text text-transparent">
                  RAJ DIGITAL
                </span>
                <p className="text-xs font-semibold text-emerald-600">Premium AI Solutions</p>
              </div>
            </div>
            
            <div className="flex items-center space-x-4">
              <a 
                href="https://github.com/rajshah9305"
                target="_blank"
                rel="noopener noreferrer"
                className="flex items-center space-x-2 text-slate-600 hover:text-emerald-600 transition-all duration-300 hover:scale-105"
              >
                <Github className="w-5 h-5" />
                <span className="hidden sm:inline text-sm font-semibold">GitHub</span>
              </a>
              <button 
                onClick={() => setShowCart(!showCart)}
                className="relative group"
              >
                <div className="relative">
                  <ShoppingCart className="w-6 h-6 text-slate-600 group-hover:text-emerald-600 transition-all duration-300 group-hover:scale-110" />
                  {cart.length > 0 && (
                    <span className="absolute -top-2 -right-2 bg-gradient-to-r from-orange-500 to-pink-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center font-bold animate-bounce">
                      {cart.length}
                    </span>
                  )}
                </div>
              </button>
              <button className="flex items-center space-x-2 px-5 py-2.5 bg-gradient-to-r from-emerald-500 via-teal-500 to-cyan-500 text-white rounded-xl hover:shadow-xl transition-all duration-300 font-semibold hover:scale-105">
                <User className="w-4 h-4" />
                <span className="hidden sm:inline">Sign In</span>
              </button>
            </div>
          </div>
        </div>
      </header>

      {/* Shopping Cart Sidebar */}
      {showCart && (
        <div className="fixed inset-0 z-50 overflow-hidden">
          <div className="absolute inset-0 bg-black/50 backdrop-blur-sm" onClick={() => setShowCart(false)}></div>
          <div className="absolute right-0 top-0 h-full w-full max-w-md bg-white shadow-2xl transform transition-transform duration-300">
            <div className="p-6 h-full flex flex-col">
              <div className="flex items-center justify-between mb-6">
                <h2 className="text-2xl font-bold text-slate-900">Your Cart</h2>
                <button onClick={() => setShowCart(false)} className="p-2 hover:bg-slate-100 rounded-lg transition">
                  <X className="w-6 h-6" />
                </button>
              </div>
              
              {cart.length === 0 ? (
                <div className="flex-1 flex flex-col items-center justify-center text-slate-500">
                  <ShoppingCart className="w-16 h-16 mb-4 opacity-50" />
                  <p className="text-lg font-medium">Your cart is empty</p>
                  <p className="text-sm">Add some amazing products!</p>
                </div>
              ) : (
                <>
                  <div className="flex-1 overflow-y-auto space-y-4 p-1">
                    {cart.map((item, index) => (
                      <div key={`${item.id}-${index}`} className="flex gap-4 p-4 bg-slate-50 rounded-xl">
                        <img src={item.image} alt={item.title} className="w-20 h-20 object-cover rounded-lg flex-shrink-0" />
                        <div className="flex-1 min-w-0">
                          <h3 className="font-semibold text-sm mb-1 line-clamp-2">{item.title}</h3>
                          <p className="text-emerald-600 font-bold">${item.price}</p>
                        </div>
                        <button onClick={() => removeFromCart(item.id)} className="text-red-500 hover:text-red-700 p-1 self-start">
                          <X className="w-5 h-5" />
                        </button>
                      </div>
                    ))}
                  </div>
                  
                  <div className="border-t pt-4 mt-4">
                    <div className="flex justify-between mb-4">
                      <span className="text-lg font-semibold">Total:</span>
                      <span className="text-2xl font-bold text-emerald-600">${cartTotal}</span>
                    </div>
                    <button className="w-full py-4 bg-gradient-to-r from-emerald-500 via-teal-500 to-cyan-500 text-white rounded-xl font-bold text-lg hover:shadow-xl transition-all duration-300 hover:scale-105">
                      Checkout Now
                    </button>
                  </div>
                </>
              )}
            </div>
          </div>
        </div>
      )}

      {/* Hero Section */}
      <section className="relative bg-gradient-to-br from-emerald-600 via-teal-600 to-cyan-600 text-white py-20 overflow-hidden">
        <div className="absolute inset-0 opacity-10">
          <div className="absolute top-0 left-0 w-96 h-96 bg-white rounded-full blur-3xl"></div>
          <div className="absolute bottom-0 right-0 w-96 h-96 bg-yellow-300 rounded-full blur-3xl"></div>
        </div>
        
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
          <div className="text-center">
            <div className="inline-flex items-center gap-2 mb-6 px-5 py-2.5 bg-white/20 backdrop-blur-md rounded-full border border-white/30">
              <Zap className="w-4 h-4 text-yellow-300" />
              <span className="text-sm font-bold">Production-Ready Open Source Projects</span>
              <Sparkles className="w-4 h-4 text-yellow-300" />
            </div>
            
            <h1 className="text-5xl md:text-7xl font-black mb-6 leading-tight">
              <span className="inline-block">Launch Your</span>
              <br />
              <span className="bg-gradient-to-r from-yellow-300 via-orange-300 to-pink-300 bg-clip-text text-transparent">
                AI Business Today
              </span>
            </h1>
            
            <p className="text-xl md:text-2xl text-emerald-100 mb-10 max-w-3xl mx-auto font-medium leading-relaxed">
              Skip months of development. Get complete, battle-tested AI solutions with full source code, 
              MIT licensing, and lifetime updates. Deploy in minutes, not months.
            </p>
            
            <div className="flex flex-col sm:flex-row gap-4 justify-center mb-16">
              <button className="group px-8 py-4 bg-white text-emerald-600 rounded-xl font-bold text-lg hover:shadow-2xl transition-all duration-300 flex items-center justify-center gap-3 hover:scale-105">
                <Sparkles className="w-5 h-5 group-hover:rotate-180 transition-transform duration-500" />
                Browse All Products
              </button>
              <a
                href="https://github.com/rajshah9305"
                target="_blank"
                rel="noopener noreferrer"
                className="px-8 py-4 bg-emerald-500/30 backdrop-blur-sm text-white rounded-xl font-bold text-lg hover:bg-emerald-500/40 transition-all duration-300 border-2 border-white/30 flex items-center justify-center gap-3 hover:scale-105"
              >
                <Github className="w-5 h-5" />
                View on GitHub
              </a>
            </div>
            
            {/* Enhanced Stats */}
            <div className="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-4xl mx-auto">
              <div className="bg-white/10 backdrop-blur-lg rounded-2xl p-8 border border-white/20 hover:bg-white/15 transition-all duration-300 hover:scale-105 group">
                <div className="flex items-center justify-center mb-3">
                  <DollarSign className="w-8 h-8 text-yellow-300 group-hover:rotate-12 transition-transform" />
                </div>
                <div className="text-4xl md:text-5xl font-black mb-2">${(totalRevenue / 1000).toFixed(1)}K+</div>
                <div className="text-emerald-100 font-semibold">Generated Revenue</div>
              </div>
              <div className="bg-white/10 backdrop-blur-lg rounded-2xl p-8 border border-white/20 hover:bg-white/15 transition-all duration-300 hover:scale-105 group">
                <div className="flex items-center justify-center mb-3">
                  <Award className="w-8 h-8 text-yellow-300 group-hover:rotate-12 transition-transform" />
                </div>
                <div className="text-4xl md:text-5xl font-black mb-2">{products.length}</div>
                <div className="text-emerald-100 font-semibold">Premium Products</div>
              </div>
              <div className="bg-white/10 backdrop-blur-lg rounded-2xl p-8 border border-white/20 hover:bg-white/15 transition-all duration-300 hover:scale-105 group">
                <div className="flex items-center justify-center mb-3">
                  <TrendingUp className="w-8 h-8 text-yellow-300 group-hover:scale-110 transition-transform" />
                </div>
                <div className="text-4xl md:text-5xl font-black mb-2">{totalSales.toLocaleString()}+</div>
                <div className="text-emerald-100 font-semibold">Happy Customers</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Search and Filters */}
      <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 -mt-10 relative z-20">
        <div className="bg-white rounded-3xl shadow-2xl p-6 border-2 border-emerald-100">
          <div className="flex flex-col lg:flex-row gap-4">
            <div className="flex-1 relative group">
              <Search className="absolute left-4 top-1/2 transform -translate-y-1/2 text-slate-400 w-5 h-5 group-focus-within:text-emerald-500 transition" />
              <input
                type="text"
                placeholder="Search for AI tools, agents, builders, and more..."
                value={searchQuery}
                onChange={(e) => setSearchQuery(e.target.value)}
                className="w-full pl-12 pr-4 py-4 border-2 border-slate-200 rounded-xl focus:ring-4 focus:ring-emerald-200 focus:border-emerald-500 outline-none transition-all duration-300 font-medium"
              />
            </div>
            <div className="flex gap-2 overflow-x-auto pb-2 lg:pb-0">
              {categories.map(category => (
                <button
                  key={category}
                  onClick={() => setSelectedCategory(category)}
                  className={`px-5 py-4 rounded-xl font-bold whitespace-nowrap transition-all duration-300 ${
                    selectedCategory === category
                      ? 'bg-gradient-to-r from-emerald-500 via-teal-500 to-cyan-500 text-white shadow-xl scale-105'
                      : 'bg-slate-100 text-slate-700 hover:bg-slate-200 hover:scale-105'
                  }`}
                >
                  {category}
                </button>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* Products Grid */}
      <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
        <div className="flex items-center justify-between mb-10">
          <div>
            <h2 className="text-4xl font-black text-slate-900 mb-2">
              {selectedCategory === 'All' ? '🚀 All Products' : `${selectedCategory}`}
            </h2>
            <p className="text-slate-600 font-medium">Production-ready solutions for modern developers</p>
          </div>
          <div className="hidden sm:flex items-center gap-2 px-4 py-2 bg-emerald-50 rounded-xl border-2 border-emerald-200">
            <TrendingUp className="w-5 h-5 text-emerald-600" />
            <span className="font-bold text-emerald-600">{filteredProducts.length} products</span>
          </div>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {filteredProducts.map(product => (
            <div 
              key={product.id} 
              className="bg-white rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition-all duration-500 transform hover:-translate-y-2 group border-2 border-transparent hover:border-emerald-200"
              onMouseEnter={() => setHoveredProduct(product.id)}
              onMouseLeave={() => setHoveredProduct(null)}
            >
              <div className="relative overflow-hidden h-56">
                <img 
                  src={product.image} 
                  alt={product.title}
                  className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700"
                />
                <div className="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                
                {product.featured && (
                  <div className="absolute top-4 left-4 bg-gradient-to-r from-yellow-400 via-orange-500 to-pink-500 text-white px-4 py-2 rounded-xl shadow-xl text-xs font-black flex items-center gap-1 animate-pulse">
                    <Star className="w-3 h-3 fill-current" />
                    FEATURED
                  </div>
                )}
                
                <div className="absolute top-4 right-4 bg-white/95 backdrop-blur-sm px-4 py-2 rounded-xl shadow-xl">
                  <div className="flex items-center space-x-1">
                    <Star className="w-4 h-4 text-yellow-500 fill-current" />
                    <span className="font-black text-slate-900">{product.rating}</span>
                  </div>
                </div>

                {hoveredProduct === product.id && (
                  <div className="absolute inset-0 flex items-center justify-center gap-3 bg-black/40 backdrop-blur-sm transition-opacity duration-300">
                    <a
                      href={product.githubUrl}
                      target="_blank"
                      rel="noopener noreferrer"
                      className="px-4 py-2 bg-white/90 backdrop-blur-sm text-slate-900 rounded-lg font-bold text-sm hover:bg-white transition flex items-center gap-2"
                    >
                      <Github className="w-4 h-4" />
                      Code
                    </a>
                    {product.demoUrl && (
                      <a
                        href={product.demoUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                        className="px-4 py-2 bg-emerald-500 text-white rounded-lg font-bold text-sm hover:bg-emerald-600 transition flex items-center gap-2"
                      >
                        <ExternalLink className="w-4 h-4" />
                        Demo
                      </a>
                    )}
                  </div>
                )}
              </div>
              
              <div className="p-6">
                <div className="flex items-center justify-between mb-3">
                  <span className="text-xs font-black text-emerald-600 bg-emerald-50 px-3 py-1.5 rounded-lg border border-emerald-200">
                    {product.category}
                  </span>
                  <span className="text-xs text-slate-500 flex items-center gap-1 font-semibold">
                    <Download className="w-3 h-3" />
                    {product.sales} sales
                  </span>
                </div>
                
                <h3 className="text-xl font-black text-slate-900 mb-3 group-hover:text-emerald-600 transition-colors duration-300 h-14 line-clamp-2">
                  {product.title}
                </h3>
                
                <p className="text-sm text-slate-600 mb-4 line-clamp-2 leading-relaxed h-10">{product.description}</p>
                
                <div className="flex flex-wrap gap-2 mb-4">
                  {product.tags.slice(0, 3).map(tag => (
                    <span key={tag} className="text-xs bg-gradient-to-r from-slate-100 to-slate-50 text-slate-700 px-3 py-1 rounded-lg font-semibold border border-slate-200">
                      {tag}
                    </span>
                  ))}
                </div>

                <div className="mb-5 space-y-2">
                  {product.features.slice(0, 3).map((feature, idx) => (
                    <div key={idx} className="flex items-center text-xs text-slate-600">
                      <div className="w-5 h-5 rounded-full bg-emerald-100 flex items-center justify-center mr-2 flex-shrink-0">
                        <Check className="w-3 h-3 text-emerald-600" />
                      </div>
                      <span className="font-medium">{feature}</span>
                    </div>
                  ))}
                </div>
                
                <div className="flex items-center justify-between pt-5 border-t-2 border-slate-100">
                  <div>
                    <div className="flex items-baseline gap-1">
                      <span className="text-3xl font-black bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text text-transparent">
                        ${product.price}
                      </span>
                      <span className="text-xs text-slate-500 font-semibold">one-time</span>
                    </div>
                    <p className="text-xs text-slate-500 mt-1">Lifetime access</p>
                  </div>
                  <button 
                    onClick={() => addToCart(product)}
                    className="px-6 py-3 bg-gradient-to-r from-emerald-500 via-teal-500 to-cyan-500 text-white rounded-xl font-bold hover:shadow-xl transform hover:scale-105 transition-all duration-300 flex items-center gap-2"
                  >
                    <ShoppingCart className="w-4 h-4" />
                    Add
                  </button>
                </div>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* Value Proposition */}
      <section className="bg-gradient-to-br from-slate-50 via-emerald-50 to-teal-50 py-20 border-y-4 border-emerald-100">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <div className="inline-flex items-center gap-2 mb-4 px-4 py-2 bg-emerald-100 rounded-full">
              <Shield className="w-4 h-4 text-emerald-600" />
              <span className="text-sm font-bold text-emerald-700">Why Developers Trust Us</span>
            </div>
            <h2 className="text-4xl md:text-5xl font-black text-slate-900 mb-4">
              Battle-Tested in Production
            </h2>
            <p className="text-xl text-slate-600 max-w-2xl mx-auto font-medium">
              Real code from real projects. No tutorials, no demos—just production-grade tools you can deploy today.
            </p>
          </div>
          
          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
            <div className="bg-white rounded-2xl p-8 shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2 border-2 border-emerald-100 group">
              <div className="w-14 h-14 bg-gradient-to-br from-emerald-500 to-teal-500 rounded-2xl flex items-center justify-center mb-5 group-hover:scale-110 transition-transform duration-300">
                <Github className="w-7 h-7 text-white" />
              </div>
              <h3 className="text-xl font-black text-slate-900 mb-3">Open Source</h3>
              <p className="text-slate-600 leading-relaxed">MIT licensed code. Full transparency with complete source access and documentation.</p>
            </div>
            
            <div className="bg-white rounded-2xl p-8 shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2 border-2 border-teal-100 group">
              <div className="w-14 h-14 bg-gradient-to-br from-teal-500 to-cyan-500 rounded-2xl flex items-center justify-center mb-5 group-hover:scale-110 transition-transform duration-300">
                <Zap className="w-7 h-7 text-white" />
              </div>
              <h3 className="text-xl font-black text-slate-900 mb-3">Production Ready</h3>
              <p className="text-slate-600 leading-relaxed">Tested in real environments. Deploy immediately and start generating revenue.</p>
            </div>
            
            <div className="bg-white rounded-2xl p-8 shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2 border-2 border-cyan-100 group">
              <div className="w-14 h-14 bg-gradient-to-br from-cyan-500 to-blue-500 rounded-2xl flex items-center justify-center mb-5 group-hover:scale-110 transition-transform duration-300">
                <Sparkles className="w-7 h-7 text-white" />
              </div>
              <h3 className="text-xl font-black text-slate-900 mb-3">Modern Stack</h3>
              <p className="text-slate-600 leading-relaxed">TypeScript, React, AWS, Cerebras. Built with cutting-edge technologies.</p>
            </div>
            
            <div className="bg-white rounded-2xl p-8 shadow-xl hover:shadow-2xl transition-all duration-300 transform hover:-translate-y-2 border-2 border-blue-100 group">
              <div className="w-14 h-14 bg-gradient-to-br from-blue-500 to-purple-500 rounded-2xl flex items-center justify-center mb-5 group-hover:scale-110 transition-transform duration-300">
                <DollarSign className="w-7 h-7 text-white" />
              </div>
              <h3 className="text-xl font-black text-slate-900 mb-3">One Payment</h3>
              <p className="text-slate-600 leading-relaxed">Pay once, own forever. No subscriptions, no hidden fees, free updates included.</p>
            </div>
          </div>
        </div>
      </section>

      {/* CTA Section */}
      <section className="relative bg-gradient-to-br from-slate-900 via-emerald-900 to-teal-900 text-white py-24 overflow-hidden">
        <div className="absolute inset-0 opacity-10">
          <div className="absolute top-1/4 left-1/4 w-96 h-96 bg-emerald-500 rounded-full blur-3xl animate-pulse"></div>
          <div className="absolute bottom-1/4 right-1/4 w-96 h-96 bg-teal-500 rounded-full blur-3xl animate-pulse" style={{animationDelay: '1s'}}></div>
        </div>
        
        <div className="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 text-center relative z-10">
          <div className="inline-flex items-center gap-2 mb-6 px-5 py-2 bg-white/10 backdrop-blur-md rounded-full border border-white/20">
            <Award className="w-4 h-4 text-yellow-300" />
            <span className="text-sm font-bold">Limited Time: Lifetime Access</span>
          </div>
          
          <h2 className="text-4xl md:text-6xl font-black mb-6 leading-tight">
            Start Building Your
            <br />
            <span className="bg-gradient-to-r from-yellow-300 via-emerald-300 to-teal-300 bg-clip-text text-transparent">
              AI Empire Today
            </span>
          </h2>
          
          <p className="text-xl md:text-2xl text-emerald-100 mb-10 max-w-3xl mx-auto leading-relaxed font-medium">
            Join 2,500+ developers who've already accelerated their AI journey. 
            One payment, instant access, lifetime updates.
          </p>
          
          <div className="flex flex-col sm:flex-row gap-5 justify-center mb-16">
            <a
              href="https://github.com/rajshah9305"
              target="_blank"
              rel="noopener noreferrer"
              className="group px-10 py-5 bg-white text-slate-900 rounded-2xl font-black text-lg hover:shadow-2xl transform hover:scale-105 transition-all duration-300 inline-flex items-center justify-center gap-3"
            >
              <Github className="w-6 h-6 group-hover:rotate-12 transition-transform" />
              Explore on GitHub
            </a>
            <button className="px-10 py-5 bg-gradient-to-r from-emerald-500 via-teal-500 to-cyan-500 text-white rounded-2xl font-black text-lg hover:shadow-2xl transform hover:scale-105 transition-all duration-300 border-2 border-white/20 inline-flex items-center justify-center gap-3">
              <Sparkles className="w-6 h-6" />
              View All Products
            </button>
          </div>
          
          <div className="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-3xl mx-auto">
            <div className="bg-white/5 backdrop-blur-lg rounded-2xl p-6 border border-white/10">
              <div className="text-4xl font-black text-emerald-300 mb-2">MIT</div>
              <div className="text-emerald-100 font-semibold">License Included</div>
            </div>
            <div className="bg-white/5 backdrop-blur-lg rounded-2xl p-6 border border-white/10">
              <div className="text-4xl font-black text-teal-300 mb-2">100%</div>
              <div className="text-teal-100 font-semibold">Source Code Access</div>
            </div>
            <div className="bg-white/5 backdrop-blur-lg rounded-2xl p-6 border border-white/10">
              <div className="text-4xl font-black text-cyan-300 mb-2">∞</div>
              <div className="text-cyan-100 font-semibold">Lifetime Updates</div>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-slate-900 text-slate-400 py-16">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid grid-cols-2 md:grid-cols-4 gap-10 mb-12">
            <div>
              <h4 className="text-white font-black mb-5 text-lg">Products</h4>
              <ul className="space-y-3 text-sm">
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">AI Tools</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Cloud Solutions</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Developer Tools</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Creative Tools</a></li>
              </ul>
            </div>
            <div>
              <h4 className="text-white font-black mb-5 text-lg">Resources</h4>
              <ul className="space-y-3 text-sm">
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Documentation</a></li>
                <li><a href="https://github.com/rajshah9305" target="_blank" rel="noopener noreferrer" className="hover:text-emerald-400 transition font-medium">GitHub</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">API Reference</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Tutorials</a></li>
              </ul>
            </div>
            <div>
              <h4 className="text-white font-black mb-5 text-lg">Support</h4>
              <ul className="space-y-3 text-sm">
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Help Center</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Contact Us</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">FAQ</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Community</a></li>
              </ul>
            </div>
            <div>
              <h4 className="text-white font-black mb-5 text-lg">Legal</h4>
              <ul className="space-y-3 text-sm">
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Terms of Service</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Privacy Policy</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Licenses</a></li>
                <li><a href="#" className="hover:text-emerald-400 transition font-medium">Refund Policy</a></li>
              </ul>
            </div>
          </div>
          
          <div className="border-t border-slate-800 pt-8">
            <div className="flex flex-col md:flex-row items-center justify-between gap-4">
              <div className="flex items-center gap-3">
                <div className="w-10 h-10 bg-gradient-to-br from-emerald-500 to-teal-500 rounded-xl flex items-center justify-center">
                  <Sparkles className="w-5 h-5 text-white" />
                </div>
                <div>
                  <p className="text-white font-bold">RAJ DIGITAL PRODUCTS</p>
                  <p className="text-xs text-slate-500">Premium AI Solutions</p>
                </div>
              </div>
              
              <div className="text-center md:text-right">
                <p className="text-sm mb-1">&copy; 2025 Raj Shah. All rights reserved.</p>
                <p className="text-xs text-slate-500">
                  Built by a senior developer. Production-ready code with full source access.
                </p>
              </div>
            </div>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default DigitalMarketplace;
