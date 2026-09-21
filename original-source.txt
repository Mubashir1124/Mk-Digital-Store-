import React, { useState, useEffect, useMemo } from 'react';
import {
  ShoppingBag, Heart, Search, User, Menu, X, Star, Truck, ShieldCheck, RefreshCw, 
  Headphones, ChevronRight, Filter, Plus, Minus, Trash2, CheckCircle2, Clock, 
  Package, MapPin, Phone, Mail, ArrowRight, SlidersHorizontal, Sparkles, ExternalLink,
  ChevronDown, Copy, Check, AlertCircle, BarChart3, Database, Tag, Settings, Eye,
  Lock, ArrowLeft, Send, CheckCircle, Percent, Zap, Smartphone, Watch, Speaker, 
  Battery, Shield, ShoppingCart, LayoutDashboard, Grid
} from 'lucide-react';

const INITIAL_PRODUCTS = [
  {
    id: 'prod-1',
    name: 'Soundcore Liberty 4 NC Earbuds',
    category: 'Earbuds',
    brand: 'Anker',
    price: 18500,
    originalPrice: 22000,
    discount: 16,
    rating: 4.8,
    reviewsCount: 142,
    inStock: true,
    stockQty: 25,
    isFeatured: true,
    isNew: true,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1590658268037-6bf12165a8df?w=600&q=80',
      'https://images.unsplash.com/photo-1606220588913-b3aacb4d2f46?w=600&q=80',
      'https://images.unsplash.com/photo-1572536147248-ac59a8abfa4b?w=600&q=80'
    ],
    description: '99.2% noise reduction with Adaptive ANC 2.0. Custom 11mm drivers delivering Hi-Res Wireless Audio and LDAC technology. 10/50 Hours super long battery life.',
    features: ['Adaptive ANC 2.0', '50 Hours Playtime', 'Hi-Res Audio LDAC', 'IPX4 Water Resistance', '6-Mic AI Clear Calls'],
    specs: { 'Bluetooth': 'v5.3', 'Driver': '11mm Custom', 'Battery': 'Up to 50 Hrs', 'Codec': 'LDAC, AAC, SBC', 'Warranty': '12 Months Official' },
    colors: ['Jet Black', 'Clear Blue', 'Velvet White']
  },
  {
    id: 'prod-2',
    name: 'HK9 Pro Plus Smart Watch Amoled',
    category: 'Smart Watches',
    brand: 'HK Series',
    price: 7499,
    originalPrice: 9999,
    discount: 25,
    rating: 4.7,
    reviewsCount: 89,
    inStock: true,
    stockQty: 18,
    isFeatured: true,
    isNew: false,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1579586337278-3befd40fd17a?w=600&q=80',
      'https://images.unsplash.com/photo-1508685096489-7aacd43bd3b1?w=600&q=80'
    ],
    description: 'Gen 3 Amoled Screen with Chat GPT Integration, AI Watch Faces, 2GB Internal ROM, Smooth Gesture Controls, and Compass sensor.',
    features: ['2.02 Inch AMOLED Screen', 'Chat GPT AI Integrated', 'Dynamic Island Notifications', 'Heart Rate & Sleep Tracking', 'Bluetooth Calling'],
    specs: { 'Display': '2.02" AMOLED (420x485)', 'Storage': '2GB ROM', 'Battery': '380 mAh (3-5 Days)', 'Waterproof': 'IP67', 'OS Support': 'Android & iOS' },
    colors: ['Titanium Silver', 'Space Black']
  },
  {
    id: 'prod-3',
    name: 'JBL Flip 6 Portable Waterproof Speaker',
    category: 'Speakers',
    brand: 'JBL',
    price: 34500,
    originalPrice: 39999,
    discount: 14,
    rating: 4.9,
    reviewsCount: 210,
    inStock: true,
    stockQty: 8,
    isFeatured: true,
    isNew: false,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?w=600&q=80',
      'https://images.unsplash.com/photo-1545454675-3531b543be5d?w=600&q=80'
    ],
    description: 'Louder, more powerful sound with 2-way speaker system. IP67 waterproof and dustproof, with 12 hours of playtime on a single charge.',
    features: ['Bold Sound & Deep Bass', 'IP67 Waterproof & Dustproof', '12 Hours Playtime', 'PartyBoost Compatible', 'USB Charging Protection'],
    specs: { 'Output': '30W RMS', 'Bluetooth': 'v5.1', 'Battery': '4800 mAh', 'Weight': '550g', 'Warranty': '6 Months Seller' },
    colors: ['Squad Camo', 'Deep Ocean Blue', 'Midnight Black']
  },
  {
    id: 'prod-4',
    name: 'Anker 20,000mAh Power Bank 87W',
    category: 'Power Banks',
    brand: 'Anker',
    price: 14999,
    originalPrice: 17500,
    discount: 14,
    rating: 4.8,
    reviewsCount: 76,
    inStock: true,
    stockQty: 30,
    isFeatured: false,
    isNew: true,
    isBestSeller: false,
    images: [
      'https://images.unsplash.com/photo-1609592424009-f806408f2a6c?w=600&q=80',
      'https://images.unsplash.com/photo-1583863788434-e58a36330cf0?w=600&q=80'
    ],
    description: 'Ultra-fast 87W max output with built-in USB-C cable. Simultaneously fast charges laptops, MacBooks, iPhones, and Android phones.',
    features: ['87W Fast Output', 'Built-in Durable USB-C Cable', 'Smart Digital Display', 'Trickle Charging Mode', 'MultiProtect Safety System'],
    specs: { 'Capacity': '20,000 mAh', 'Ports': '2x USB-C, 1x USB-A', 'Max Output': '87W Total', 'Weight': '395g', 'Warranty': '18 Months Official' },
    colors: ['Matte Black', 'Ice White']
  },
  {
    id: 'prod-5',
    name: 'Baseus 65W GaN Fast Charger 3-Port',
    category: 'Chargers',
    brand: 'Baseus',
    price: 6800,
    originalPrice: 8500,
    discount: 20,
    rating: 4.6,
    reviewsCount: 54,
    inStock: true,
    stockQty: 40,
    isFeatured: false,
    isNew: false,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1583863788434-e58a36330cf0?w=600&q=80',
      'https://images.unsplash.com/photo-1622445268465-8438a058d880?w=600&q=80'
    ],
    description: 'GaN5 technology delivering compact 65W fast charging for laptops, tablets, and mobile devices with dual USB-C and single USB-A slots.',
    features: ['65W High Power Output', 'GaN 5th Gen Tech', '3 Device Simultaneous Charge', 'Temperature Control 2.0', 'Universal PK Plug'],
    specs: { 'Ports': '2 Type-C + 1 USB-A', 'Input': 'AC 100-240V', 'Tech': 'GaN Pro Fast Charging', 'Dimensions': '98x36x32mm', 'Warranty': '6 Months' },
    colors: ['Midnight Black', 'Snow White']
  },
  {
    id: 'prod-6',
    name: 'Logitech G Pro X Superlight Mouse',
    category: 'Gaming Accessories',
    brand: 'Logitech',
    price: 38900,
    originalPrice: 44000,
    discount: 11,
    rating: 4.9,
    reviewsCount: 188,
    inStock: true,
    stockQty: 12,
    isFeatured: true,
    isNew: false,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1615663245857-ac93bb7c39e7?w=600&q=80',
      'https://images.unsplash.com/photo-1527864550417-7fd91fc51a46?w=600&q=80'
    ],
    description: 'Ultra-lightweight wireless esports gaming mouse under 63 grams with HERO 25K Sensor and LIGHTSPEED zero latency wireless tech.',
    features: ['Ultra-Lightweight <63g', 'HERO 25K Sensor (25,600 DPI)', 'Zero Additive PTFE Feet', '70 Hours Battery Life', 'LIGHTSPEED Wireless'],
    specs: { 'Sensor': 'HERO 25K', 'DPI': '100 - 25,600 DPI', 'Report Rate': '1000Hz (1ms)', 'Battery': '70 hrs', 'Weight': '63 grams' },
    colors: ['Matte Black', 'Pure White', 'Magenta Pink']
  },
  {
    id: 'prod-7',
    name: 'Redragon K552 RGB Mechanical Keyboard',
    category: 'Gaming Accessories',
    brand: 'Redragon',
    price: 11500,
    originalPrice: 14000,
    discount: 18,
    rating: 4.5,
    reviewsCount: 95,
    inStock: true,
    stockQty: 15,
    isFeatured: false,
    isNew: false,
    isBestSeller: false,
    images: [
      'https://images.unsplash.com/photo-1587829741301-dc798b83add3?w=600&q=80',
      'https://images.unsplash.com/photo-1511467687858-23d96c32e4ae?w=600&q=80'
    ],
    description: 'Compact 87 Keys Tenkeyless Mechanical Gaming Keyboard with Dustproof Blue Switches, Metal Construction, and Rainbow RGB Backlighting.',
    features: ['Mechanical Blue Switches', 'Rainbow RGB Backlit', 'TKL Compact 87 Key Design', 'Aircraft-grade Aluminum Plate', 'Anti-Ghosting N-Key Rollover'],
    specs: { 'Switch Type': 'Dustproof Blue', 'Keycaps': 'Double-shot Injection', 'Connection': 'Gold-plated USB', 'Cable Length': '1.8m', 'Warranty': '1 Year' },
    colors: ['Black RGB', 'White RGB']
  },
  {
    id: 'prod-8',
    name: 'Sony WH-1000XM5 Noise Canceling Headphones',
    category: 'Headphones',
    brand: 'Sony',
    price: 112000,
    originalPrice: 125000,
    discount: 10,
    rating: 4.9,
    reviewsCount: 312,
    inStock: true,
    stockQty: 5,
    isFeatured: true,
    isNew: true,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=600&q=80',
      'https://images.unsplash.com/photo-1484704849700-f032a568e944?w=600&q=80'
    ],
    description: 'Industry-leading noise canceling with 8 microphones and Auto NC Optimizer. Ultra-comfortable lightweight design with soft fit leather.',
    features: ['2 Processors & 8 Microphones', 'Ultra-clear Hands-free Calls', 'Up to 30-hour Battery', 'Touch Control Panel', 'Multipoint Connection'],
    specs: { 'Driver': '30mm Dynamic', 'Battery': '30 Hours (NC On)', 'Bluetooth': 'v5.2', 'Weight': '250g', 'Warranty': '1 Year Official' },
    colors: ['Black', 'Silver', 'Midnight Blue']
  },
  {
    id: 'prod-9',
    name: 'Baseus Aluminum Desktop Folding Phone Stand',
    category: 'Mobile Accessories',
    brand: 'Baseus',
    price: 2200,
    originalPrice: 2900,
    discount: 24,
    rating: 4.7,
    reviewsCount: 68,
    inStock: true,
    stockQty: 50,
    isFeatured: false,
    isNew: false,
    isBestSeller: false,
    images: [
      'https://images.unsplash.com/photo-1586105251261-72a756497a11?w=600&q=80'
    ],
    description: 'Heavy-duty foldable aluminum alloy desktop phone & tablet holder with 360-degree height & angle adjustments and silicone pads.',
    features: ['Full Aluminum Alloy Alloy', 'Foldable & Pocket Sized', 'Non-slip Rubber Base', 'Cable Pass-through Slot', 'Supports 4.7" - 12.9" Devices'],
    specs: { 'Material': 'Aluminum + Silicone', 'Weight': '180g', 'Adjustability': 'Dual Axis 180°', 'Color': 'Space Grey' },
    colors: ['Space Grey', 'Silver']
  },
  {
    id: 'prod-10',
    name: 'Ugreen 7-in-1 USB-C Hub Adapter 4K 60Hz',
    category: 'Computer Accessories',
    brand: 'Ugreen',
    price: 9800,
    originalPrice: 12000,
    discount: 18,
    rating: 4.8,
    reviewsCount: 41,
    inStock: true,
    stockQty: 22,
    isFeatured: false,
    isNew: true,
    isBestSeller: false,
    images: [
      'https://images.unsplash.com/photo-1544652478-6653e09f18a2?w=600&q=80'
    ],
    description: 'Expand your laptop with 4K@60Hz HDMI, 100W Power Delivery USB-C, 2x USB 3.0 (5Gbps), Gigabit Ethernet RJ45, and SD/TF Card Reader.',
    features: ['4K @ 60Hz HDMI Output', '100W PD Fast Charging', '1000Mbps Ethernet Port', 'SD & Micro SD Card Reader', '5Gbps SuperSpeed USB 3.0'],
    specs: { 'Input': 'USB-C Cable', 'Output': 'HDMI, PD, RJ45, 2x USB 3.0, SD, MicroSD', 'Material': 'Aluminum Shell', 'Warranty': '6 Months' },
    colors: ['Deep Silver']
  },
  {
    id: 'prod-11',
    name: 'Smart RGB Corner Floor Lamp Wi-Fi & App Control',
    category: 'Smart Gadgets',
    brand: 'MK Tech',
    price: 12500,
    originalPrice: 16000,
    discount: 22,
    rating: 4.6,
    reviewsCount: 39,
    inStock: true,
    stockQty: 14,
    isFeatured: true,
    isNew: true,
    isBestSeller: false,
    images: [
      'https://images.unsplash.com/photo-1507473885765-e6ed057f782c?w=600&q=80'
    ],
    description: '16 Million Color changing corner floor ambient lamp with Music Sync, Alexa/Google Assistant compatibility, and RF Remote control.',
    features: ['16 Million Colors + Dynamic Modes', 'Music Sync Reactive LED', 'Tuya Smart App & Remote Control', 'Voice Control Compatible', 'Durable Aluminum Frame'],
    specs: { 'Height': '140 cm', 'Power': '20W LED', 'Connectivity': 'Wi-Fi 2.4GHz + Bluetooth', 'Voltage': '220V PK Plug', 'Warranty': '6 Months' },
    colors: ['Black Metal']
  },
  {
    id: 'prod-12',
    name: 'Joyroom 100W Braided Type-C to Type-C Cable 2m',
    category: 'Mobile Accessories',
    brand: 'Joyroom',
    price: 1850,
    originalPrice: 2500,
    discount: 26,
    rating: 4.7,
    reviewsCount: 110,
    inStock: true,
    stockQty: 100,
    isFeatured: false,
    isNew: false,
    isBestSeller: true,
    images: [
      'https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?w=600&q=80'
    ],
    description: 'Heavy duty high-density nylon braided 100W 5A Fast Charging PD Cable with LED Wattage Power display indicator.',
    features: ['100W Super Fast Charging', 'Real-time LED Power Display', 'High Density Nylon Braided', '480Mbps Data Transfer', 'E-Marker Smart Chip'],
    specs: { 'Length': '2 Meters', 'Power Output': '20V/5A Max (100W)', 'Compatibility': 'Laptops, MacBooks, Mobiles', 'Warranty': '3 Months Replacement' },
    colors: ['Obsidian Black']
  }
];

const CATEGORIES = [
  { name: 'Smart Watches', icon: Watch, count: '18 Items', image: 'https://images.unsplash.com/photo-1579586337278-3befd40fd17a?w=300&q=80' },
  { name: 'Earbuds', icon: Headphones, count: '24 Items', image: 'https://images.unsplash.com/photo-1590658268037-6bf12165a8df?w=300&q=80' },
  { name: 'Headphones', icon: Headphones, count: '12 Items', image: 'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=300&q=80' },
  { name: 'Mobile Accessories', icon: Smartphone, count: '45 Items', image: 'https://images.unsplash.com/photo-1586105251261-72a756497a11?w=300&q=80' },
  { name: 'Chargers', icon: Zap, count: '30 Items', image: 'https://images.unsplash.com/photo-1583863788434-e58a36330cf0?w=300&q=80' },
  { name: 'Power Banks', icon: Battery, count: '15 Items', image: 'https://images.unsplash.com/photo-1609592424009-f806408f2a6c?w=300&q=80' },
  { name: 'Speakers', icon: Speaker, count: '10 Items', image: 'https://images.unsplash.com/photo-1608043152269-423dbba4e7e1?w=300&q=80' },
  { name: 'Computer Accessories', icon: Grid, count: '28 Items', image: 'https://images.unsplash.com/photo-1544652478-6653e09f18a2?w=300&q=80' },
  { name: 'Gaming Accessories', icon: Zap, count: '32 Items', image: 'https://images.unsplash.com/photo-1615663245857-ac93bb7c39e7?w=300&q=80' },
  { name: 'Smart Gadgets', icon: Sparkles, count: '16 Items', image: 'https://images.unsplash.com/photo-1507473885765-e6ed057f782c?w=300&q=80' }
];

const PAKISTAN_CITIES = [
  'Islamabad', 'Rawalpindi', 'Lahore', 'Karachi', 'Faisalabad', 'Multan',
  'Peshawar', 'Quetta', 'Sialkot', 'Gujranwala', 'Hyderabad', 'Abbottabad'
];

export default function App() {
  // Navigation & View state
  const [currentTab, setCurrentTab] = useState('home'); // home, shop, product-detail, cart, checkout, tracking, account, admin, wishlist, about, contact, faq, privacy, terms, db-schema
  const [selectedProductId, setSelectedProductId] = useState('prod-1');
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [searchQuery, setSearchQuery] = useState('');
  const [showSearchDropdown, setShowSearchDropdown] = useState(false);

  // E-commerce state
  const [products, setProducts] = useState(INITIAL_PRODUCTS);
  const [cart, setCart] = useState([]);
  const [wishlist, setWishlist] = useState(['prod-1', 'prod-6']);
  const [appliedCoupon, setAppliedCoupon] = useState(null);
  const [couponInput, setCouponInput] = useState('');
  const [toastMessage, setToastMessage] = useState(null);

  // User & Orders State
  const [user, setUser] = useState({ name: 'Hamza Khan', email: 'hamza@example.pk', phone: '0300-1234567', loggedIn: true, role: 'admin' });
  const [orders, setOrders] = useState([
    {
      id: 'MK-89421',
      date: '2026-09-18',
      items: [
        { ...INITIAL_PRODUCTS[0], qty: 1, selectedColor: 'Jet Black' },
        { ...INITIAL_PRODUCTS[4], qty: 1, selectedColor: 'Midnight Black' }
      ],
      subtotal: 25300,
      shipping: 250,
      discount: 1000,
      total: 24550,
      paymentMethod: 'Cash on Delivery',
      status: 'Shipped', // Order Placed, Confirmed, Processing, Shipped, Out for Delivery, Delivered
      customer: {
        name: 'Hamza Khan',
        phone: '0300-1234567',
        email: 'hamza@example.pk',
        address: 'House # 42, Street 10, F-11/1',
        city: 'Islamabad',
        province: 'Federal Capital'
      },
      trackingNo: 'TCS-99182374'
    }
  ]);

  // Flash Sale Timer State
  const [timeLeft, setTimeLeft] = useState({ days: 2, hours: 14, minutes: 35, seconds: 48 });

  useEffect(() => {
    const timer = setInterval(() => {
      setTimeLeft(prev => {
        if (prev.seconds > 0) return { ...prev, seconds: prev.seconds - 1 };
        if (prev.minutes > 0) return { ...prev, minutes: 59, seconds: 59 };
        if (prev.hours > 0) return { ...prev, hours: prev.hours - 1, minutes: 59, seconds: 59 };
        if (prev.days > 0) return { ...prev, days: prev.days - 1, hours: 23, minutes: 59, seconds: 59 };
        return prev;
      });
    }, 1000);
    return () => clearInterval(timer);
  }, []);

  // Helper Toast function
  const triggerToast = (msg) => {
    setToastMessage(msg);
    setTimeout(() => setToastMessage(null), 3000);
  };

  // Currency Formatter
  const formatPKR = (amount) => {
    return 'Rs. ' + amount.toLocaleString('en-PK');
  };

  // Cart Handlers
  const addToCart = (product, color = null, qty = 1) => {
    const targetColor = color || (product.colors ? product.colors[0] : 'Default');
    setCart(prev => {
      const existing = prev.find(item => item.id === product.id && item.selectedColor === targetColor);
      if (existing) {
        return prev.map(item =>
          item.id === product.id && item.selectedColor === targetColor
            ? { ...item, qty: item.qty + qty }
            : item
        );
      }
      return [...prev, { ...product, qty, selectedColor: targetColor }];
    });
    triggerToast(`Added "${product.name}" to Cart!`);
  };

  const updateCartQty = (id, color, delta) => {
    setCart(prev =>
      prev.map(item => {
        if (item.id === id && item.selectedColor === color) {
          const newQty = item.qty + delta;
          return newQty > 0 ? { ...item, qty: newQty } : null;
        }
        return item;
      }).filter(Boolean)
    );
  };

  const removeFromCart = (id, color) => {
    setCart(prev => prev.filter(item => !(item.id === id && item.selectedColor === color)));
    triggerToast('Item removed from cart');
  };

  const toggleWishlist = (productId) => {
    setWishlist(prev => {
      if (prev.includes(productId)) {
        triggerToast('Removed from Wishlist');
        return prev.filter(id => id !== productId);
      } else {
        triggerToast('Added to Wishlist!');
        return [...prev, productId];
      }
    });
  };

  // Filtered products calculation for shop
  const [shopCategory, setShopCategory] = useState('All');
  const [shopPriceMax, setShopPriceMax] = useState(120000);
  const [shopSort, setShopSort] = useState('featured');
  const [shopInStockOnly, setShopInStockOnly] = useState(false);

  const filteredProducts = useMemo(() => {
    return products.filter(p => {
      if (shopCategory !== 'All' && p.category !== shopCategory) return false;
      if (p.price > shopPriceMax) return false;
      if (shopInStockOnly && !p.inStock) return false;
      if (searchQuery.trim() !== '') {
        const query = searchQuery.toLowerCase();
        return p.name.toLowerCase().includes(query) || p.category.toLowerCase().includes(query) || p.brand.toLowerCase().includes(query);
      }
      return true;
    }).sort((a, b) => {
      if (shopSort === 'price-low') return a.price - b.price;
      if (shopSort === 'price-high') return b.price - a.price;
      if (shopSort === 'rating') return b.rating - a.rating;
      if (shopSort === 'newest') return (b.isNew ? 1 : 0) - (a.isNew ? 1 : 0);
      return (b.isFeatured ? 1 : 0) - (a.isFeatured ? 1 : 0);
    });
  }, [products, shopCategory, shopPriceMax, shopInStockOnly, shopSort, searchQuery]);

  // Selected product object
  const selectedProduct = products.find(p => p.id === selectedProductId) || products[0];

  // Cart Calculations
  const cartSubtotal = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
  const estimatedShipping = cartSubtotal > 3000 || cartSubtotal === 0 ? 0 : 250;
  const couponDiscountAmount = appliedCoupon ? Math.round((cartSubtotal * appliedCoupon.percentage) / 100) : 0;
  const cartGrandTotal = Math.max(0, cartSubtotal + estimatedShipping - couponDiscountAmount);

  return (
    <div className="min-h-screen bg-slate-950 text-slate-100 font-sans selection:bg-cyan-500 selection:text-slate-950 flex flex-col">
      {/* Toast Notification Popup */}
      {toastMessage && (
        <div className="fixed top-20 right-4 z-50 bg-cyan-500 text-slate-950 px-5 py-3 rounded-xl shadow-2xl font-bold flex items-center space-x-2 animate-bounce">
          <CheckCircle2 className="w-5 h-5 text-slate-950" />
          <span>{toastMessage}</span>
        </div>
      )}

      {/* Top Announcement Bar */}
      <div className="bg-gradient-to-r from-cyan-600 via-blue-600 to-indigo-600 text-white text-xs font-medium py-2 px-4 text-center flex justify-between items-center px-4 md:px-12">
        <div className="hidden md:flex items-center space-x-4">
          <span className="flex items-center"><Phone className="w-3.5 h-3.5 mr-1" /> WhatsApp / Helpline: +92 300 1234567</span>
          <span className="flex items-center"><MapPin className="w-3.5 h-3.5 mr-1" /> Fast Delivery across Pakistan</span>
        </div>
        <div className="w-full md:w-auto text-center font-semibold tracking-wide">
          🇵🇰 FREE Shipping across Pakistan on orders over Rs. 3,000! Cash on Delivery Available
        </div>
        <div className="hidden md:flex items-center space-x-3 text-xs">
          <button onClick={() => setCurrentTab('db-schema')} className="hover:underline flex items-center bg-black/20 px-2 py-0.5 rounded text-cyan-200">
            <Database className="w-3 h-3 mr-1" /> DB Schema Architecture
          </button>
        </div>
      </div>

      {/* Main Header / Navigation */}
      <header className="sticky top-0 z-40 bg-slate-900/90 backdrop-blur-md border-b border-slate-800 transition-all">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between gap-4">
          
          {/* Logo */}
          <div className="flex items-center space-x-3 cursor-pointer" onClick={() => setCurrentTab('home')}>
            <div className="w-11 h-11 bg-gradient-to-tr from-cyan-500 to-blue-600 rounded-xl flex items-center justify-center text-slate-950 font-black text-2xl shadow-lg shadow-cyan-500/20">
              MK
            </div>
            <div>
              <span className="text-xl font-extrabold tracking-tight text-white block leading-none">
                MK DIGITAL <span className="text-cyan-400">STORE</span>
              </span>
              <span className="text-[10px] text-slate-400 tracking-widest uppercase font-semibold">
                Pakistan's Premium Tech Hub
              </span>
            </div>
          </div>

          {/* Search Bar - Center Desktop */}
          <div className="hidden lg:flex flex-1 max-w-lg relative">
            <input
              type="text"
              placeholder="Search earbuds, smart watches, fast chargers..."
              value={searchQuery}
              onChange={(e) => {
                setSearchQuery(e.target.value);
                setShowSearchDropdown(e.target.value.length > 0);
              }}
              onFocus={() => searchQuery && setShowSearchDropdown(true)}
              className="w-full bg-slate-950/80 border border-slate-700/80 rounded-full py-2.5 pl-5 pr-12 text-sm text-slate-200 placeholder-slate-500 focus:outline-none focus:border-cyan-500 focus:ring-1 focus:ring-cyan-500 transition"
            />
            <button 
              onClick={() => { setCurrentTab('shop'); setShowSearchDropdown(false); }}
              className="absolute right-1.5 top-1.5 bottom-1.5 bg-cyan-500 hover:bg-cyan-400 text-slate-950 px-4 rounded-full font-bold flex items-center justify-center transition"
            >
              <Search className="w-4 h-4" />
            </button>

            {/* Instant Search Autocomplete Dropdown */}
            {showSearchDropdown && (
              <div className="absolute top-12 left-0 right-0 bg-slate-900 border border-slate-800 rounded-2xl shadow-2xl p-2 z-50 max-h-96 overflow-y-auto">
                <div className="px-3 py-2 text-xs font-semibold text-slate-400 border-b border-slate-800 flex justify-between">
                  <span>Matching Products</span>
                  <button onClick={() => setShowSearchDropdown(false)} className="text-slate-500 hover:text-slate-300">Close</button>
                </div>
                {filteredProducts.length === 0 ? (
                  <div className="p-4 text-center text-sm text-slate-500">No products found matching "{searchQuery}"</div>
                ) : (
                  filteredProducts.slice(0, 5).map(p => (
                    <div
                      key={p.id}
                      onClick={() => {
                        setSelectedProductId(p.id);
                        setCurrentTab('product-detail');
                        setShowSearchDropdown(false);
                      }}
                      className="p-2.5 hover:bg-slate-800/80 rounded-xl flex items-center space-x-3 cursor-pointer transition"
                    >
                      <img src={p.images[0]} alt={p.name} className="w-10 h-10 object-cover rounded-lg" />
                      <div className="flex-1 min-w-0">
                        <div className="text-sm font-medium text-slate-200 truncate">{p.name}</div>
                        <div className="text-xs text-cyan-400 font-semibold">{formatPKR(p.price)}</div>
                      </div>
                    </div>
                  ))
                )}
              </div>
            )}
          </div>

          {/* Desktop Nav Actions */}
          <div className="hidden md:flex items-center space-x-6 text-sm">
            <button 
              onClick={() => setCurrentTab('shop')} 
              className={`hover:text-cyan-400 transition font-medium ${currentTab === 'shop' ? 'text-cyan-400 font-bold' : 'text-slate-300'}`}
            >
              Shop
            </button>
            <button 
              onClick={() => setCurrentTab('tracking')} 
              className={`hover:text-cyan-400 transition font-medium flex items-center ${currentTab === 'tracking' ? 'text-cyan-400 font-bold' : 'text-slate-300'}`}
            >
              <Package className="w-4 h-4 mr-1 text-cyan-400" /> Track Order
            </button>
            
            {user?.role === 'admin' && (
              <button 
                onClick={() => setCurrentTab('admin')} 
                className="bg-indigo-600/30 text-indigo-400 border border-indigo-500/40 px-3 py-1.5 rounded-lg hover:bg-indigo-600/50 transition font-medium flex items-center text-xs"
              >
                <LayoutDashboard className="w-3.5 h-3.5 mr-1" /> Admin Panel
              </button>
            )}

            {/* Icons Actions */}
            <div className="flex items-center space-x-4 pl-4 border-l border-slate-800">
              {/* Wishlist Icon */}
              <button 
                onClick={() => setCurrentTab('wishlist')} 
                className="relative p-2 text-slate-300 hover:text-cyan-400 transition"
                title="Wishlist"
              >
                <Heart className="w-6 h-6" />
                {wishlist.length > 0 && (
                  <span className="absolute top-0 right-0 w-5 h-5 bg-pink-500 text-white rounded-full text-[10px] font-bold flex items-center justify-center">
                    {wishlist.length}
                  </span>
                )}
              </button>

              {/* Shopping Cart Icon */}
              <button 
                onClick={() => setCurrentTab('cart')} 
                className="relative p-2 text-slate-300 hover:text-cyan-400 transition"
                title="Cart"
              >
                <ShoppingBag className="w-6 h-6" />
                {cart.length > 0 && (
                  <span className="absolute top-0 right-0 w-5 h-5 bg-cyan-500 text-slate-950 rounded-full text-[10px] font-bold flex items-center justify-center">
                    {cart.reduce((s, i) => s + i.qty, 0)}
                  </span>
                )}
              </button>

              {/* Account Button */}
              <button 
                onClick={() => setCurrentTab('account')} 
                className="flex items-center space-x-2 text-slate-300 hover:text-cyan-400 transition"
              >
                <div className="w-8 h-8 rounded-full bg-slate-800 border border-slate-700 flex items-center justify-center">
                  <User className="w-4 h-4 text-cyan-400" />
                </div>
              </button>
            </div>
          </div>

          {/* Mobile Hamburger Button */}
          <div className="flex md:hidden items-center space-x-3">
            <button 
              onClick={() => setCurrentTab('cart')} 
              className="relative p-2 text-slate-300"
            >
              <ShoppingBag className="w-6 h-6" />
              {cart.length > 0 && (
                <span className="absolute top-0 right-0 w-4 h-4 bg-cyan-500 text-slate-950 rounded-full text-[9px] font-bold flex items-center justify-center">
                  {cart.reduce((s, i) => s + i.qty, 0)}
                </span>
              )}
            </button>
            <button 
              onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
              className="p-2 text-slate-300 focus:outline-none"
            >
              {mobileMenuOpen ? <X className="w-7 h-7 text-cyan-400" /> : <Menu className="w-7 h-7" />}
            </button>
          </div>

        </div>

        {/* Mobile Search Bar Row */}
        <div className="px-4 pb-3 lg:hidden">
          <div className="relative">
            <input
              type="text"
              placeholder="Search products..."
              value={searchQuery}
              onChange={(e) => {
                setSearchQuery(e.target.value);
                setShowSearchDropdown(e.target.value.length > 0);
              }}
              className="w-full bg-slate-950 border border-slate-800 rounded-xl py-2 pl-4 pr-10 text-sm text-slate-200 placeholder-slate-500 focus:outline-none focus:border-cyan-500"
            />
            <Search className="w-4 h-4 absolute right-3 top-3 text-slate-500" />
          </div>
        </div>
      </header>

      {/* Mobile Drawer Menu Overlay */}
      {mobileMenuOpen && (
        <div className="fixed inset-0 z-50 bg-slate-950/95 backdrop-blur-xl flex flex-col p-6 md:hidden animate-in fade-in slide-in-from-top-5">
          <div className="flex justify-between items-center pb-6 border-b border-slate-800">
            <span className="font-bold text-lg text-white">Navigation</span>
            <button onClick={() => setMobileMenuOpen(false)} className="p-2 text-slate-400">
              <X className="w-6 h-6" />
            </button>
          </div>
          <div className="flex flex-col space-y-4 my-6 text-lg font-semibold">
            <button onClick={() => { setCurrentTab('home'); setMobileMenuOpen(false); }} className="text-left py-2 border-b border-slate-900 text-cyan-400">Home</button>
            <button onClick={() => { setCurrentTab('shop'); setMobileMenuOpen(false); }} className="text-left py-2 border-b border-slate-900 text-slate-200">Shop Catalog</button>
            <button onClick={() => { setCurrentTab('tracking'); setMobileMenuOpen(false); }} className="text-left py-2 border-b border-slate-900 text-slate-200">Track Order</button>
            <button onClick={() => { setCurrentTab('wishlist'); setMobileMenuOpen(false); }} className="text-left py-2 border-b border-slate-900 text-slate-200">Wishlist ({wishlist.length})</button>
            <button onClick={() => { setCurrentTab('account'); setMobileMenuOpen(false); }} className="text-left py-2 border-b border-slate-900 text-slate-200">My Account</button>
            <button onClick={() => { setCurrentTab('db-schema'); setMobileMenuOpen(false); }} className="text-left py-2 border-b border-slate-900 text-slate-400 text-sm flex items-center">
              <Database className="w-4 h-4 mr-2" /> Database Schema Specs
            </button>
            {user?.role === 'admin' && (
              <button onClick={() => { setCurrentTab('admin'); setMobileMenuOpen(false); }} className="text-left py-2 text-indigo-400 flex items-center">
                <LayoutDashboard className="w-5 h-5 mr-2" /> Admin Dashboard
              </button>
            )}
          </div>
          <div className="mt-auto pt-6 border-t border-slate-800 text-sm text-slate-400">
            <p className="font-semibold text-slate-200">Helpline / WhatsApp:</p>
            <p className="text-cyan-400 font-bold text-base mt-1">+92 300 1234567</p>
          </div>
        </div>
      )}

      {/* Dynamic Content Views */}
      <main className="flex-1">

        {/* ==================== 1. HOMEPAGE VIEW ==================== */}
        {currentTab === 'home' && (
          <div className="space-y-16 pb-16">
            
            {}
            {/* Hero Section */}
            <section className="relative overflow-hidden bg-gradient-to-b from-slate-900 via-slate-950 to-slate-950 pt-8 pb-16 border-b border-slate-800/80">
              <div className="absolute top-0 right-0 w-96 h-96 bg-cyan-500/10 rounded-full blur-3xl -z-10 pointer-events-none"></div>
              <div className="absolute bottom-0 left-1/4 w-80 h-80 bg-blue-600/10 rounded-full blur-3xl -z-10 pointer-events-none"></div>

              <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid md:grid-cols-2 gap-12 items-center">
                <div className="space-y-6 text-center md:text-left">
                  <div className="inline-flex items-center space-x-2 bg-cyan-500/10 border border-cyan-500/30 px-3.5 py-1.5 rounded-full text-cyan-400 text-xs font-bold uppercase tracking-wider">
                    <Sparkles className="w-3.5 h-3.5" />
                    <span>Next-Gen Tech In Pakistan</span>
                  </div>
                  <h1 className="text-4xl sm:text-5xl lg:text-6xl font-black text-white tracking-tight leading-tight">
                    Upgrade Your Tech. <br />
                    <span className="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-blue-500 to-indigo-400">
                      Upgrade Your Life.
                    </span>
                  </h1>
                  <p className="text-slate-400 text-base sm:text-lg max-w-xl mx-auto md:mx-0 leading-relaxed">
                    Discover 100% original wireless earbuds, smart watches, fast chargers & premium gaming accessories with official warranty and nationwide Cash on Delivery.
                  </p>
                  <div className="flex flex-col sm:flex-row items-center justify-center md:justify-start gap-4 pt-2">
                    <button 
                      onClick={() => setCurrentTab('shop')} 
                      className="w-full sm:w-auto bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold px-8 py-4 rounded-xl shadow-lg shadow-cyan-500/25 transition flex items-center justify-center space-x-2 text-base"
                    >
                      <span>Shop Gadgets Now</span>
                      <ArrowRight className="w-5 h-5" />
                    </button>
                    <button 
                      onClick={() => {
                        const el = document.getElementById('flash-sale');
                        el?.scrollIntoView({ behavior: 'smooth' });
                      }} 
                      className="w-full sm:w-auto bg-slate-800/80 hover:bg-slate-800 border border-slate-700 text-slate-200 font-semibold px-6 py-4 rounded-xl transition flex items-center justify-center space-x-2 text-base"
                    >
                      <span>Explore Mega Deals</span>
                      <Zap className="w-4 h-4 text-cyan-400" />
                    </button>
                  </div>
                  {/* Trust Badges */}
                  <div className="pt-6 grid grid-cols-3 gap-4 text-center md:text-left border-t border-slate-800/60">
                    <div>
                      <p className="text-xl font-bold text-white">100%</p>
                      <p className="text-xs text-slate-400">Original Products</p>
                    </div>
                    <div>
                      <p className="text-xl font-bold text-cyan-400">24-48 Hours</p>
                      <p className="text-xs text-slate-400">Fast Dispatch</p>
                    </div>
                    <div>
                      <p className="text-xl font-bold text-white">COD</p>
                      <p className="text-xs text-slate-400">Available All PK</p>
                    </div>
                  </div>
                </div>

                {/* Hero Feature Product Card Banner */}
                <div className="relative flex justify-center">
                  <div className="relative w-full max-w-md bg-gradient-to-b from-slate-900 to-slate-950 border border-slate-800 rounded-3xl p-6 shadow-2xl overflow-hidden group">
                    <span className="absolute top-4 left-4 bg-red-500 text-white text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider z-10">
                      HOT DEAL -25%
                    </span>
                    <img 
                      src="https://images.unsplash.com/photo-1579586337278-3befd40fd17a?w=600&q=80" 
                      alt="HK9 Pro Plus" 
                      className="w-full h-64 object-contain my-4 transform group-hover:scale-105 transition duration-500" 
                    />
                    <div className="space-y-2">
                      <span className="text-xs text-cyan-400 font-semibold uppercase tracking-widest">Featured Smartwatch</span>
                      <h3 className="text-xl font-bold text-white">HK9 Pro Plus Amoled Chat GPT</h3>
                      <div className="flex items-center space-x-3">
                        <span className="text-2xl font-black text-cyan-400">Rs. 7,499</span>
                        <span className="text-sm text-slate-500 line-through">Rs. 9,999</span>
                      </div>
                      <button 
                        onClick={() => { setSelectedProductId('prod-2'); setCurrentTab('product-detail'); }}
                        className="w-full mt-4 bg-slate-800 hover:bg-slate-700 text-white font-semibold py-2.5 rounded-xl border border-slate-700 transition"
                      >
                        View Product Details
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </section>

            {}
            {/* Categories Grid */}
            <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="flex justify-between items-end mb-8">
                <div>
                  <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Shop By Category</h2>
                  <p className="text-sm text-slate-400 mt-1">Explore our wide selection of tech categories</p>
                </div>
                <button onClick={() => setCurrentTab('shop')} className="text-cyan-400 hover:text-cyan-300 text-sm font-semibold flex items-center">
                  View All <ChevronRight className="w-4 h-4 ml-1" />
                </button>
              </div>

              <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-4">
                {CATEGORIES.map((cat, idx) => {
                  const IconComp = cat.icon;
                  return (
                    <div
                      key={idx}
                      onClick={() => {
                        setShopCategory(cat.name);
                        setCurrentTab('shop');
                      }}
                      className="bg-slate-900 border border-slate-800 hover:border-cyan-500/50 rounded-2xl p-4 flex flex-col items-center text-center cursor-pointer group transition duration-300 hover:shadow-xl hover:shadow-cyan-500/5"
                    >
                      <div className="w-14 h-14 rounded-2xl bg-slate-800 flex items-center justify-center text-cyan-400 group-hover:bg-cyan-500 group-hover:text-slate-950 transition duration-300 mb-3">
                        <IconComp className="w-7 h-7" />
                      </div>
                      <h3 className="font-bold text-sm text-slate-200 group-hover:text-cyan-400 transition">{cat.name}</h3>
                      <p className="text-xs text-slate-500 mt-1">{cat.count}</p>
                    </div>
                  );
                })}
              </div>
            </section>

            {/* FLASH SALE SECTION WITH LIVE COUNTDOWN */}
            <section id="flash-sale" className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="bg-gradient-to-r from-red-950/60 via-slate-900 to-slate-900 border border-red-900/50 rounded-3xl p-6 sm:p-8 relative overflow-hidden">
                <div className="flex flex-col md:flex-row md:items-center justify-between gap-6 mb-8 pb-6 border-b border-slate-800">
                  <div className="flex items-center space-x-3">
                    <div className="p-3 bg-red-600/20 text-red-500 rounded-2xl border border-red-500/30">
                      <Zap className="w-8 h-8 animate-pulse" />
                    </div>
                    <div>
                      <h2 className="text-2xl sm:text-3xl font-black text-white uppercase tracking-tight">Flash Sale</h2>
                      <p className="text-xs text-slate-400">Limited time offers with massive price drops!</p>
                    </div>
                  </div>

                  {/* Countdown Box */}
                  <div className="flex items-center space-x-3 bg-slate-950/80 px-4 py-3 rounded-2xl border border-slate-800 self-start md:self-auto">
                    <span className="text-xs uppercase font-bold text-slate-400 mr-2">Ends In:</span>
                    <div className="flex items-center space-x-2 text-center font-mono font-bold">
                      <div className="bg-red-950 text-red-400 px-2.5 py-1 rounded-lg border border-red-800/50 text-sm">{String(timeLeft.days).padStart(2, '0')}<span className="text-[10px] block font-sans text-slate-500">Days</span></div>
                      <span className="text-red-500">:</span>
                      <div className="bg-red-950 text-red-400 px-2.5 py-1 rounded-lg border border-red-800/50 text-sm">{String(timeLeft.hours).padStart(2, '0')}<span className="text-[10px] block font-sans text-slate-500">Hrs</span></div>
                      <span className="text-red-500">:</span>
                      <div className="bg-red-950 text-red-400 px-2.5 py-1 rounded-lg border border-red-800/50 text-sm">{String(timeLeft.minutes).padStart(2, '0')}<span className="text-[10px] block font-sans text-slate-500">Min</span></div>
                      <span className="text-red-500">:</span>
                      <div className="bg-red-950 text-red-400 px-2.5 py-1 rounded-lg border border-red-800/50 text-sm">{String(timeLeft.seconds).padStart(2, '0')}<span className="text-[10px] block font-sans text-slate-500">Sec</span></div>
                    </div>
                  </div>
                </div>

                {/* Flash Products Grid */}
                <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                  {products.slice(0, 4).map(product => (
                    <ProductCard 
                      key={product.id}
                      product={product}
                      onSelect={(id) => { setSelectedProductId(id); setCurrentTab('product-detail'); }}
                      onAddToCart={(p) => addToCart(p)}
                      onToggleWishlist={(id) => toggleWishlist(id)}
                      isWishlisted={wishlist.includes(product.id)}
                      formatPKR={formatPKR}
                    />
                  ))}
                </div>
              </div>
            </section>

            {/* FEATURED PRODUCTS SECTION */}
            <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="flex justify-between items-end mb-8">
                <div>
                  <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Best Sellers & Featured</h2>
                  <p className="text-sm text-slate-400 mt-1">Highest rated gadgets recommended by our customers</p>
                </div>
                <button onClick={() => setCurrentTab('shop')} className="text-cyan-400 hover:text-cyan-300 text-sm font-semibold flex items-center">
                  Explore Full Shop <ChevronRight className="w-4 h-4 ml-1" />
                </button>
              </div>

              <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                {products.filter(p => p.isBestSeller || p.isFeatured).slice(0, 8).map(product => (
                  <ProductCard 
                    key={product.id}
                    product={product}
                    onSelect={(id) => { setSelectedProductId(id); setCurrentTab('product-detail'); }}
                    onAddToCart={(p) => addToCart(p)}
                    onToggleWishlist={(id) => toggleWishlist(id)}
                    isWishlisted={wishlist.includes(product.id)}
                    formatPKR={formatPKR}
                  />
                ))}
              </div>
            </section>

            {}
            {/* WHY CHOOSE US / TRUST GUARANTEE */}
            <section className="bg-slate-900 border-y border-slate-800 py-12">
              <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div className="grid grid-cols-2 md:grid-cols-4 gap-8">
                  <div className="flex flex-col items-center text-center p-4">
                    <div className="w-12 h-12 rounded-2xl bg-cyan-500/10 text-cyan-400 flex items-center justify-center mb-4">
                      <Truck className="w-6 h-6" />
                    </div>
                    <h4 className="font-bold text-white text-base">Cash on Delivery</h4>
                    <p className="text-xs text-slate-400 mt-1">Pay at your doorstep anywhere across Pakistan</p>
                  </div>
                  <div className="flex flex-col items-center text-center p-4">
                    <div className="w-12 h-12 rounded-2xl bg-cyan-500/10 text-cyan-400 flex items-center justify-center mb-4">
                      <ShieldCheck className="w-6 h-6" />
                    </div>
                    <h4 className="font-bold text-white text-base">100% Original Products</h4>
                    <p className="text-xs text-slate-400 mt-1">Direct official brand warranty & authenticity guarantee</p>
                  </div>
                  <div className="flex flex-col items-center text-center p-4">
                    <div className="w-12 h-12 rounded-2xl bg-cyan-500/10 text-cyan-400 flex items-center justify-center mb-4">
                      <RefreshCw className="w-6 h-6" />
                    </div>
                    <h4 className="font-bold text-white text-base">7 Days Replacement</h4>
                    <p className="text-xs text-slate-400 mt-1">Hassle-free 7-day checking replacement policy</p>
                  </div>
                  <div className="flex flex-col items-center text-center p-4">
                    <div className="w-12 h-12 rounded-2xl bg-cyan-500/10 text-cyan-400 flex items-center justify-center mb-4">
                      <Headphones className="w-6 h-6" />
                    </div>
                    <h4 className="font-bold text-white text-base">24/7 Dedicated Support</h4>
                    <p className="text-xs text-slate-400 mt-1">WhatsApp & phone support whenever you need</p>
                  </div>
                </div>
              </div>
            </section>

            {/* CUSTOMER REVIEWS TESTIMONIALS */}
            <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="text-center max-w-2xl mx-auto mb-12">
                <h2 className="text-3xl font-extrabold text-white">Loved By Tech Enthusiasts</h2>
                <p className="text-slate-400 text-sm mt-2">Read real reviews from our verified buyers across Karachi, Lahore, Islamabad and more.</p>
              </div>

              <div className="grid md:grid-cols-3 gap-6">
                {[
                  { name: 'Usman Chaudhry', city: 'Lahore', rating: 5, review: 'Super fast delivery! Received my Anker Liberty 4 NC in just 2 days in Lahore. 100% original product with official warranty claim card.', product: 'Soundcore Liberty 4 NC' },
                  { name: 'Ayesha Malik', city: 'Islamabad', rating: 5, review: 'Ordered the HK9 Pro Plus Amoled smartwatch. Sound quality on call is crystal clear and ChatGPT feature works surprisingly well!', product: 'HK9 Pro Plus Smart Watch' },
                  { name: 'Bilal Ahmed', city: 'Karachi', rating: 5, review: 'Best store for original tech accessories in Pakistan. COD made it super trustworthy. Will buy again!', product: 'JBL Flip 6 Speaker' }
                ].map((rev, idx) => (
                  <div key={idx} className="bg-slate-900 border border-slate-800 rounded-2xl p-6 space-y-4">
                    <div className="flex justify-between items-center">
                      <div>
                        <h4 className="font-bold text-white text-sm">{rev.name}</h4>
                        <span className="text-xs text-cyan-400">{rev.city}, Pakistan</span>
                      </div>
                      <div className="flex text-amber-400">
                        {[...Array(rev.rating)].map((_, i) => (
                          <Star key={i} className="w-4 h-4 fill-amber-400" />
                        ))}
                      </div>
                    </div>
                    <p className="text-slate-300 text-xs leading-relaxed italic">"{rev.review}"</p>
                    <div className="pt-2 border-t border-slate-800 text-[11px] text-slate-500 font-semibold">
                      Verified Purchase: <span className="text-slate-300">{rev.product}</span>
                    </div>
                  </div>
                ))}
              </div>
            </section>

            {/* NEWSLETTER SUBSCRIBE */}
            <section className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="bg-gradient-to-r from-cyan-900/40 via-slate-900 to-blue-950/40 border border-cyan-500/20 rounded-3xl p-8 sm:p-12 text-center space-y-6">
                <div className="w-14 h-14 bg-cyan-500/20 text-cyan-400 rounded-2xl flex items-center justify-center mx-auto">
                  <Mail className="w-7 h-7" />
                </div>
                <h2 className="text-2xl sm:text-3xl font-extrabold text-white">Subscribe For VIP Deals & Coupon Codes</h2>
                <p className="text-slate-400 text-sm max-w-lg mx-auto">Get notified about flash sales, secret promo codes, and new tech drops directly in your inbox.</p>
                <form 
                  onSubmit={(e) => { e.preventDefault(); triggerToast('Subscribed successfully!'); }} 
                  className="max-w-md mx-auto flex flex-col sm:flex-row gap-3"
                >
                  <input
                    type="email"
                    required
                    placeholder="Enter your email address..."
                    className="flex-1 bg-slate-950 border border-slate-700 rounded-xl px-4 py-3 text-sm text-slate-200 placeholder-slate-500 focus:outline-none focus:border-cyan-500"
                  />
                  <button type="submit" className="bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold px-6 py-3 rounded-xl transition">
                    Subscribe
                  </button>
                </form>
              </div>
            </section>

          </div>
        )}

        {/* ==================== 2. SHOP CATALOG PAGE ==================== */}
        {}
        {currentTab === 'shop' && (
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div className="mb-6">
              <h1 className="text-3xl font-extrabold text-white">All Products Catalog</h1>
              <p className="text-slate-400 text-sm mt-1">Showing {filteredProducts.length} items available across Pakistan</p>
            </div>

            <div className="grid lg:grid-cols-4 gap-8">
              {/* Sidebar Filters */}
              <div className="bg-slate-900 border border-slate-800 rounded-2xl p-6 h-fit space-y-6">
                <div className="flex justify-between items-center border-b border-slate-800 pb-4">
                  <h3 className="font-bold text-white flex items-center text-base">
                    <Filter className="w-4 h-4 mr-2 text-cyan-400" /> Filters
                  </h3>
                  <button 
                    onClick={() => {
                      setShopCategory('All');
                      setShopPriceMax(120000);
                      setShopInStockOnly(false);
                      setSearchQuery('');
                    }} 
                    className="text-xs text-cyan-400 hover:underline"
                  >
                    Reset All
                  </button>
                </div>

                {/* Category Filter */}
                <div className="space-y-2">
                  <label className="text-xs font-bold uppercase tracking-wider text-slate-400">Category</label>
                  <div className="space-y-1">
                    <button
                      onClick={() => setShopCategory('All')}
                      className={`w-full text-left px-3 py-2 rounded-lg text-xs font-medium transition ${shopCategory === 'All' ? 'bg-cyan-500 text-slate-950 font-bold' : 'text-slate-300 hover:bg-slate-800'}`}
                    >
                      All Categories ({products.length})
                    </button>
                    {CATEGORIES.map((cat, idx) => (
                      <button
                        key={idx}
                        onClick={() => setShopCategory(cat.name)}
                        className={`w-full text-left px-3 py-2 rounded-lg text-xs font-medium transition ${shopCategory === cat.name ? 'bg-cyan-500 text-slate-950 font-bold' : 'text-slate-300 hover:bg-slate-800'}`}
                      >
                        {cat.name}
                      </button>
                    ))}
                  </div>
                </div>

                {/* Price Range Filter */}
                <div className="space-y-3 border-t border-slate-800 pt-4">
                  <div className="flex justify-between text-xs font-bold">
                    <span className="uppercase text-slate-400">Max Price</span>
                    <span className="text-cyan-400">{formatPKR(shopPriceMax)}</span>
                  </div>
                  <input
                    type="range"
                    min="1000"
                    max="120000"
                    step="1000"
                    value={shopPriceMax}
                    onChange={(e) => setShopPriceMax(Number(e.target.value))}
                    className="w-full accent-cyan-500 cursor-pointer"
                  />
                </div>

                {/* In Stock Toggle */}
                <div className="flex items-center justify-between border-t border-slate-800 pt-4">
                  <span className="text-xs font-bold uppercase text-slate-400">In Stock Only</span>
                  <input
                    type="checkbox"
                    checked={shopInStockOnly}
                    onChange={(e) => setShopInStockOnly(e.target.checked)}
                    className="w-4 h-4 accent-cyan-500 rounded cursor-pointer"
                  />
                </div>
              </div>

              {/* Main Products Grid */}
              <div className="lg:col-span-3 space-y-6">
                {/* Sort Bar */}
                <div className="bg-slate-900 border border-slate-800 rounded-xl p-4 flex flex-col sm:flex-row justify-between items-center gap-4">
                  <div className="text-xs text-slate-400">
                    Active Category: <span className="text-cyan-400 font-bold">{shopCategory}</span>
                  </div>
                  <div className="flex items-center space-x-3 w-full sm:w-auto">
                    <span className="text-xs text-slate-400 font-medium whitespace-nowrap">Sort By:</span>
                    <select
                      value={shopSort}
                      onChange={(e) => setShopSort(e.target.value)}
                      className="bg-slate-950 border border-slate-800 text-xs text-slate-200 rounded-lg p-2.5 focus:outline-none focus:border-cyan-500 w-full sm:w-auto"
                    >
                      <option value="featured">Featured First</option>
                      <option value="price-low">Price: Low to High</option>
                      <option value="price-high">Price: High to Low</option>
                      <option value="rating">Highest Rated</option>
                      <option value="newest">New Arrivals</option>
                    </select>
                  </div>
                </div>

                {/* Grid */}
                {filteredProducts.length === 0 ? (
                  <div className="bg-slate-900 border border-slate-800 rounded-2xl p-12 text-center space-y-4">
                    <AlertCircle className="w-12 h-12 text-slate-600 mx-auto" />
                    <h3 className="text-lg font-bold text-white">No products found</h3>
                    <p className="text-slate-400 text-xs">Try adjusting your filters or price slider.</p>
                  </div>
                ) : (
                  <div className="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-6">
                    {filteredProducts.map(product => (
                      <ProductCard 
                        key={product.id}
                        product={product}
                        onSelect={(id) => { setSelectedProductId(id); setCurrentTab('product-detail'); }}
                        onAddToCart={(p) => addToCart(p)}
                        onToggleWishlist={(id) => toggleWishlist(id)}
                        isWishlisted={wishlist.includes(product.id)}
                        formatPKR={formatPKR}
                      />
                    ))}
                  </div>
                )}
              </div>
            </div>
          </div>
        )}

        {/* ==================== 3. PRODUCT DETAILS PAGE ==================== */}
        {}
        {currentTab === 'product-detail' && selectedProduct && (
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-12">
            {/* Breadcrumb */}
            <div className="flex items-center space-x-2 text-xs text-slate-400">
              <span className="cursor-pointer hover:text-white" onClick={() => setCurrentTab('home')}>Home</span>
              <ChevronRight className="w-3 h-3" />
              <span className="cursor-pointer hover:text-white" onClick={() => setCurrentTab('shop')}>Shop</span>
              <ChevronRight className="w-3 h-3" />
              <span className="text-cyan-400 font-medium">{selectedProduct.name}</span>
            </div>

            {/* Main Product Layout */}
            <div className="grid lg:grid-cols-2 gap-10">
              
              {/* Product Images Gallery */}
              <div className="space-y-4">
                <ProductImageGallery images={selectedProduct.images} altText={selectedProduct.name} />
              </div>

              {/* Product Info & Purchase Actions */}
              <div className="space-y-6">
                <div>
                  <span className="text-xs font-bold uppercase tracking-widest text-cyan-400">{selectedProduct.brand} • {selectedProduct.category}</span>
                  <h1 className="text-2xl sm:text-3xl font-extrabold text-white mt-1">{selectedProduct.name}</h1>
                  
                  {/* Rating & Reviews */}
                  <div className="flex items-center space-x-3 mt-3">
                    <div className="flex text-amber-400 items-center">
                      <Star className="w-4 h-4 fill-amber-400" />
                      <span className="ml-1 text-sm font-bold text-white">{selectedProduct.rating}</span>
                    </div>
                    <span className="text-xs text-slate-500">({selectedProduct.reviewsCount} verified reviews)</span>
                    <span className="text-slate-700">|</span>
                    <span className={`text-xs font-bold px-2.5 py-0.5 rounded-full ${selectedProduct.inStock ? 'bg-emerald-500/10 text-emerald-400 border border-emerald-500/20' : 'bg-red-500/10 text-red-400'}`}>
                      {selectedProduct.inStock ? `In Stock (${selectedProduct.stockQty} left)` : 'Out of Stock'}
                    </span>
                  </div>
                </div>

                {/* Price Display */}
                <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5 flex items-center justify-between">
                  <div>
                    <div className="text-3xl font-black text-cyan-400">{formatPKR(selectedProduct.price)}</div>
                    {selectedProduct.originalPrice && (
                      <div className="text-sm text-slate-500 line-through mt-0.5">
                        {formatPKR(selectedProduct.originalPrice)}
                      </div>
                    )}
                  </div>
                  {selectedProduct.discount && (
                    <div className="bg-red-500 text-white font-bold text-sm px-3 py-1.5 rounded-xl uppercase">
                      Save {selectedProduct.discount}%
                    </div>
                  )}
                </div>

                <p className="text-slate-300 text-sm leading-relaxed">{selectedProduct.description}</p>

                {/* Colors Variant Selector */}
                {selectedProduct.colors && (
                  <div className="space-y-2">
                    <label className="text-xs font-bold text-slate-400 uppercase tracking-wider">Select Color Variant:</label>
                    <div className="flex space-x-3">
                      {selectedProduct.colors.map((clr, idx) => (
                        <button
                          key={idx}
                          className="px-4 py-2 text-xs font-semibold rounded-xl bg-slate-900 border border-slate-700 text-slate-200 hover:border-cyan-500 transition"
                        >
                          {clr}
                        </button>
                      ))}
                    </div>
                  </div>
                )}

                {/* Action CTA Buttons */}
                <div className="flex flex-col sm:flex-row gap-4 pt-4 border-t border-slate-800">
                  <button
                    onClick={() => addToCart(selectedProduct)}
                    className="flex-1 bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold py-4 rounded-xl shadow-lg shadow-cyan-500/20 transition flex items-center justify-center space-x-2"
                  >
                    <ShoppingBag className="w-5 h-5" />
                    <span>Add To Cart</span>
                  </button>
                  <button
                    onClick={() => {
                      addToCart(selectedProduct);
                      setCurrentTab('checkout');
                    }}
                    className="flex-1 bg-emerald-600 hover:bg-emerald-500 text-white font-bold py-4 rounded-xl transition flex items-center justify-center space-x-2"
                  >
                    <Zap className="w-5 h-5" />
                    <span>Buy Now (Express COD)</span>
                  </button>
                  <button
                    onClick={() => toggleWishlist(selectedProduct.id)}
                    className={`p-4 rounded-xl border transition flex items-center justify-center ${wishlist.includes(selectedProduct.id) ? 'bg-pink-500/10 border-pink-500 text-pink-500' : 'bg-slate-900 border-slate-800 text-slate-400 hover:text-white'}`}
                  >
                    <Heart className="w-6 h-6" />
                  </button>
                </div>

                {/* Pakistani Delivery Calculator Estimate */}
                <div className="bg-slate-900/60 border border-slate-800 rounded-2xl p-5 space-y-3">
                  <h4 className="font-bold text-white text-sm flex items-center">
                    <Truck className="w-4 h-4 mr-2 text-cyan-400" /> Delivery Estimate across Pakistan
                  </h4>
                  <div className="grid grid-cols-2 gap-3 text-xs">
                    <div className="bg-slate-950 p-3 rounded-xl">
                      <span className="text-slate-400 block font-medium">Islamabad / Rawalpindi</span>
                      <span className="text-white font-bold mt-1 block">24 Hours Express</span>
                    </div>
                    <div className="bg-slate-950 p-3 rounded-xl">
                      <span className="text-slate-400 block font-medium">Lahore, Karachi & Major Cities</span>
                      <span className="text-white font-bold mt-1 block">2-3 Working Days</span>
                    </div>
                  </div>
                </div>

              </div>
            </div>

            {/* Specifications & Features Tabs */}
            <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 sm:p-8 space-y-6">
              <h3 className="text-xl font-bold text-white border-b border-slate-800 pb-4">Key Features & Technical Specifications</h3>
              
              <div className="grid md:grid-cols-2 gap-8">
                <div>
                  <h4 className="text-sm font-bold text-cyan-400 uppercase tracking-wider mb-4">Highlights</h4>
                  <ul className="space-y-2.5">
                    {selectedProduct.features.map((feat, idx) => (
                      <li key={idx} className="flex items-center text-sm text-slate-300">
                        <CheckCircle2 className="w-4 h-4 text-cyan-400 mr-2 flex-shrink-0" />
                        <span>{feat}</span>
                      </li>
                    ))}
                  </ul>
                </div>

                <div>
                  <h4 className="text-sm font-bold text-cyan-400 uppercase tracking-wider mb-4">Technical Specs</h4>
                  <div className="space-y-2">
                    {Object.entries(selectedProduct.specs).map(([key, val], idx) => (
                      <div key={idx} className="flex justify-between py-2 border-b border-slate-800/60 text-xs">
                        <span className="text-slate-400 font-medium">{key}</span>
                        <span className="text-white font-semibold">{val}</span>
                      </div>
                    ))}
                  </div>
                </div>
              </div>
            </div>

          </div>
        )}

        {/* ==================== 4. SHOPPING CART ==================== */}
        {}
        {currentTab === 'cart' && (
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
            <h1 className="text-3xl font-extrabold text-white mb-8">Shopping Cart ({cart.reduce((s, i) => s + i.qty, 0)} Items)</h1>

            {cart.length === 0 ? (
              <div className="bg-slate-900 border border-slate-800 rounded-3xl p-16 text-center space-y-6 max-w-xl mx-auto">
                <div className="w-20 h-20 bg-slate-800 rounded-full flex items-center justify-center mx-auto text-slate-500">
                  <ShoppingCart className="w-10 h-10" />
                </div>
                <h3 className="text-2xl font-bold text-white">Your Cart is Empty</h3>
                <p className="text-slate-400 text-sm">Explore our top tech deals and add items to your cart now.</p>
                <button
                  onClick={() => setCurrentTab('shop')}
                  className="bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold px-8 py-3 rounded-xl transition"
                >
                  Start Shopping
                </button>
              </div>
            ) : (
              <div className="grid lg:grid-cols-3 gap-8">
                {/* Cart Items List */}
                <div className="lg:col-span-2 space-y-4">
                  {cart.map((item, idx) => (
                    <div key={`${item.id}-${item.selectedColor}`} className="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5 flex gap-4 items-center">
                      <img src={item.images[0]} alt={item.name} className="w-20 h-20 object-cover rounded-xl bg-slate-950" />
                      <div className="flex-1 min-w-0 space-y-1">
                        <h4 className="font-bold text-white text-base truncate">{item.name}</h4>
                        <div className="text-xs text-slate-400">Variant: <span className="text-cyan-400">{item.selectedColor}</span></div>
                        <div className="text-sm font-black text-cyan-400">{formatPKR(item.price)}</div>
                      </div>

                      {/* Quantity Controls */}
                      <div className="flex items-center space-x-3 bg-slate-950 px-3 py-1.5 rounded-xl border border-slate-800">
                        <button onClick={() => updateCartQty(item.id, item.selectedColor, -1)} className="text-slate-400 hover:text-white">
                          <Minus className="w-3.5 h-3.5" />
                        </button>
                        <span className="text-xs font-bold text-white w-4 text-center">{item.qty}</span>
                        <button onClick={() => updateCartQty(item.id, item.selectedColor, 1)} className="text-slate-400 hover:text-white">
                          <Plus className="w-3.5 h-3.5" />
                        </button>
                      </div>

                      <button onClick={() => removeFromCart(item.id, item.selectedColor)} className="p-2 text-slate-500 hover:text-red-400 transition">
                        <Trash2 className="w-5 h-5" />
                      </button>
                    </div>
                  ))}
                </div>

                {/* Cart Order Summary Sidebar */}
                <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 h-fit space-y-6">
                  <h3 className="font-bold text-white text-lg border-b border-slate-800 pb-4">Order Summary</h3>

                  {/* Promo Coupon Form */}
                  <div className="space-y-2">
                    <label className="text-xs font-semibold text-slate-400">Apply Promo Coupon:</label>
                    <div className="flex gap-2">
                      <input
                        type="text"
                        placeholder="Try PAKISTAN or FLASH10"
                        value={couponInput}
                        onChange={(e) => setCouponInput(e.target.value.toUpperCase())}
                        className="bg-slate-950 border border-slate-800 rounded-xl px-3 py-2 text-xs text-slate-200 placeholder-slate-600 focus:outline-none focus:border-cyan-500 flex-1 uppercase"
                      />
                      <button
                        onClick={() => {
                          if (couponInput === 'PAKISTAN' || couponInput === 'FLASH10') {
                            setAppliedCoupon({ code: couponInput, percentage: 10 });
                            triggerToast('Coupon Applied: 10% Discount!');
                          } else {
                            triggerToast('Invalid Promo Code');
                          }
                        }}
                        className="bg-slate-800 hover:bg-slate-700 text-xs font-bold text-white px-4 rounded-xl border border-slate-700"
                      >
                        Apply
                      </button>
                    </div>
                    {appliedCoupon && (
                      <div className="text-xs text-emerald-400 font-semibold flex justify-between items-center pt-1">
                        <span>Active Coupon: {appliedCoupon.code} (-{appliedCoupon.percentage}%)</span>
                        <button onClick={() => setAppliedCoupon(null)} className="text-slate-500 hover:text-slate-300">Remove</button>
                      </div>
                    )}
                  </div>

                  {/* Price Breakdown */}
                  <div className="space-y-3 border-t border-slate-800 pt-4 text-xs">
                    <div className="flex justify-between text-slate-400">
                      <span>Subtotal</span>
                      <span className="text-white font-semibold">{formatPKR(cartSubtotal)}</span>
                    </div>
                    <div className="flex justify-between text-slate-400">
                      <span>Estimated Shipping (Pakistan)</span>
                      <span className="text-white font-semibold">
                        {estimatedShipping === 0 ? <span className="text-emerald-400 font-bold">FREE</span> : formatPKR(estimatedShipping)}
                      </span>
                    </div>
                    {appliedCoupon && (
                      <div className="flex justify-between text-emerald-400 font-semibold">
                        <span>Discount ({appliedCoupon.percentage}%)</span>
                        <span>-{formatPKR(couponDiscountAmount)}</span>
                      </div>
                    )}
                    <div className="flex justify-between text-base font-extrabold text-white border-t border-slate-800 pt-3">
                      <span>Grand Total</span>
                      <span className="text-cyan-400">{formatPKR(cartGrandTotal)}</span>
                    </div>
                  </div>

                  <button
                    onClick={() => setCurrentTab('checkout')}
                    className="w-full bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold py-4 rounded-xl shadow-lg shadow-cyan-500/20 transition flex items-center justify-center space-x-2"
                  >
                    <span>Proceed To Checkout</span>
                    <ArrowRight className="w-5 h-5" />
                  </button>
                </div>
              </div>
            )}
          </div>
        )}

        {/* ==================== 5. CHECKOUT PAGE ==================== */}
        {}
        {currentTab === 'checkout' && (
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
            <h1 className="text-3xl font-extrabold text-white mb-8">Checkout Order</h1>

            <CheckoutView 
              cart={cart}
              cartGrandTotal={cartGrandTotal}
              formatPKR={formatPKR}
              onOrderPlaced={(newOrder) => {
                setOrders([newOrder, ...orders]);
                setCart([]);
                setCurrentTab('order-confirmation');
              }}
            />
          </div>
        )}

        {/* ==================== 6. ORDER CONFIRMATION PAGE ==================== */}
        {currentTab === 'order-confirmation' && orders.length > 0 && (
          <div className="max-w-3xl mx-auto px-4 py-16 text-center space-y-8">
            <div className="w-20 h-20 bg-emerald-500/10 text-emerald-400 border border-emerald-500/30 rounded-full flex items-center justify-center mx-auto">
              <CheckCircle2 className="w-10 h-10 animate-bounce" />
            </div>

            <div className="space-y-2">
              <h1 className="text-3xl font-black text-white">Order Placed Successfully!</h1>
              <p className="text-slate-400 text-sm">Thank you for shopping with MK Digital Store. Your order has been registered.</p>
              <div className="text-cyan-400 font-mono font-bold text-lg pt-2">Order ID: {orders[0].id}</div>
            </div>

            {/* Summary Box */}
            <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 text-left space-y-4">
              <h3 className="font-bold text-white text-base border-b border-slate-800 pb-3">Delivery Information</h3>
              <div className="grid sm:grid-cols-2 gap-4 text-xs text-slate-300">
                <div>
                  <span className="text-slate-500 block font-semibold">Customer Name:</span>
                  <span className="text-white font-medium">{orders[0].customer.name}</span>
                </div>
                <div>
                  <span className="text-slate-500 block font-semibold">Phone / WhatsApp:</span>
                  <span className="text-white font-medium">{orders[0].customer.phone}</span>
                </div>
                <div>
                  <span className="text-slate-500 block font-semibold">Address:</span>
                  <span className="text-white font-medium">{orders[0].customer.address}, {orders[0].customer.city}</span>
                </div>
                <div>
                  <span className="text-slate-500 block font-semibold">Payment Method:</span>
                  <span className="text-cyan-400 font-bold">{orders[0].paymentMethod}</span>
                </div>
              </div>
            </div>

            <div className="flex justify-center space-x-4">
              <button
                onClick={() => setCurrentTab('tracking')}
                className="bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold px-8 py-3 rounded-xl transition"
              >
                Track My Order
              </button>
              <button
                onClick={() => setCurrentTab('home')}
                className="bg-slate-800 hover:bg-slate-700 text-white font-bold px-8 py-3 rounded-xl border border-slate-700 transition"
              >
                Back To Home
              </button>
            </div>
          </div>
        )}

        {/* ==================== 7. ORDER TRACKING PAGE ==================== */}
        {}
        {currentTab === 'tracking' && (
          <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12 space-y-10">
            <div className="text-center space-y-2">
              <h1 className="text-3xl font-extrabold text-white">Track Your Order Status</h1>
              <p className="text-slate-400 text-sm">Enter your Order Reference ID (e.g. MK-89421) and registered phone number</p>
            </div>

            {/* Tracking Search Input Form */}
            <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 sm:p-8 space-y-4 shadow-xl">
              <div className="grid sm:grid-cols-2 gap-4">
                <div>
                  <label className="text-xs font-bold text-slate-400 uppercase">Order ID</label>
                  <input
                    type="text"
                    defaultValue="MK-89421"
                    className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-3 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
                  />
                </div>
                <div>
                  <label className="text-xs font-bold text-slate-400 uppercase">Phone Number</label>
                  <input
                    type="text"
                    defaultValue="0300-1234567"
                    className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-3 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
                  />
                </div>
              </div>
              <button className="w-full bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold py-3.5 rounded-xl transition">
                Check Live Tracking
              </button>
            </div>

            {/* Tracking Timeline Output */}
            <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 sm:p-8 space-y-8">
              <div className="flex flex-col sm:flex-row justify-between border-b border-slate-800 pb-6 gap-4">
                <div>
                  <div className="text-xs text-slate-500 uppercase font-bold">Active Tracking Order</div>
                  <div className="text-xl font-bold text-white mt-1">Order #MK-89421</div>
                  <div className="text-xs text-cyan-400 mt-0.5">Courier Courier Partner: TCS Express (Ref: TCS-99182374)</div>
                </div>
                <div className="text-left sm:text-right">
                  <span className="bg-cyan-500/10 text-cyan-400 border border-cyan-500/30 px-3 py-1 rounded-full text-xs font-bold">
                    In Transit (Shipped)
                  </span>
                  <div className="text-xs text-slate-400 mt-1">Est. Delivery: Tomorrow by 5:00 PM</div>
                </div>
              </div>

              {/* Visual Timeline Steps */}
              <div className="space-y-6 relative before:absolute before:inset-0 before:left-3.5 before:w-0.5 before:bg-slate-800">
                {[
                  { title: 'Order Placed', desc: 'Received order on website', time: '18 Sep, 02:30 PM', done: true },
                  { title: 'Order Confirmed', desc: 'Verified details via WhatsApp call', time: '18 Sep, 03:10 PM', done: true },
                  { title: 'Processing & Packing', desc: 'Items packed & quality tested', time: '19 Sep, 10:00 AM', done: true },
                  { title: 'Shipped via TCS', desc: 'Handed over to courier hub in Rawalpindi', time: '19 Sep, 04:45 PM', done: true },
                  { title: 'Out for Delivery', desc: 'Rider assigned for doorstep delivery', time: 'Pending', done: false },
                  { title: 'Delivered', desc: 'Payment received & completed', time: 'Pending', done: false }
                ].map((step, idx) => (
                  <div key={idx} className="relative flex items-start space-x-4 pl-8">
                    <div className={`absolute left-0 w-7 h-7 rounded-full flex items-center justify-center text-xs font-bold ${step.done ? 'bg-cyan-500 text-slate-950' : 'bg-slate-800 text-slate-500 border border-slate-700'}`}>
                      {step.done ? <Check className="w-4 h-4" /> : idx + 1}
                    </div>
                    <div className="flex-1">
                      <div className="font-bold text-sm text-white">{step.title}</div>
                      <div className="text-xs text-slate-400 mt-0.5">{step.desc}</div>
                    </div>
                    <div className="text-xs font-mono text-slate-500">{step.time}</div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}

        {/* ==================== 8. WISHLIST PAGE ==================== */}
        {currentTab === 'wishlist' && (
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
            <h1 className="text-3xl font-extrabold text-white mb-8">My Wishlist ({wishlist.length})</h1>

            {wishlist.length === 0 ? (
              <div className="bg-slate-900 border border-slate-800 rounded-3xl p-16 text-center space-y-4 max-w-md mx-auto">
                <Heart className="w-12 h-12 text-slate-600 mx-auto" />
                <h3 className="text-xl font-bold text-white">Your Wishlist is Empty</h3>
                <button onClick={() => setCurrentTab('shop')} className="bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold px-6 py-2.5 rounded-xl text-sm">
                  Explore Products
                </button>
              </div>
            ) : (
              <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                {products.filter(p => wishlist.includes(p.id)).map(product => (
                  <ProductCard 
                    key={product.id}
                    product={product}
                    onSelect={(id) => { setSelectedProductId(id); setCurrentTab('product-detail'); }}
                    onAddToCart={(p) => addToCart(p)}
                    onToggleWishlist={(id) => toggleWishlist(id)}
                    isWishlisted={true}
                    formatPKR={formatPKR}
                  />
                ))}
              </div>
            )}
          </div>
        )}

        {/* ==================== 9. ADMIN DASHBOARD ==================== */}
        {}
        {currentTab === 'admin' && (
          <AdminDashboard 
            products={products} 
            orders={orders}
            setProducts={setProducts}
            setOrders={setOrders}
            formatPKR={formatPKR}
            onViewDBSchema={() => setCurrentTab('db-schema')}
          />
        )}

        {/* ==================== 10. DB SCHEMA ARCHITECTURE DOCUMENTATION ==================== */}
        {currentTab === 'db-schema' && (
          <DatabaseSchemaView />
        )}

      </main>

      {/* Floating WhatsApp Action Button */}
      <a
        href="https://wa.me/923001234567?text=Hi%20MK%20Digital%20Store!%20I%20have%20an%20inquiry%20regarding%20products."
        target="_blank"
        rel="noopener noreferrer"
        className="fixed bottom-6 right-6 z-50 bg-emerald-500 hover:bg-emerald-400 text-white p-4 rounded-full shadow-2xl transition transform hover:scale-110 flex items-center justify-center border-2 border-emerald-400/40"
        title="Chat on WhatsApp"
      >
        <Phone className="w-6 h-6 fill-current" />
      </a>

      {}
      {/* Site Footer */}
      <footer className="bg-slate-900 border-t border-slate-800 text-slate-400 text-xs py-12">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 md:grid-cols-4 gap-8">
          <div className="space-y-3">
            <div className="flex items-center space-x-2">
              <div className="w-8 h-8 bg-cyan-500 rounded-lg flex items-center justify-center text-slate-950 font-black text-lg">
                MK
              </div>
              <span className="text-base font-bold text-white">MK Digital Store</span>
            </div>
            <p className="text-slate-400 leading-relaxed">
              Pakistan's trusted online destination for premium audio, smart watches, fast chargers & tech gadgets.
            </p>
          </div>

          <div>
            <h4 className="font-bold text-white text-sm mb-3">Quick Links</h4>
            <ul className="space-y-2">
              <li><button onClick={() => setCurrentTab('shop')} className="hover:text-cyan-400">All Gadgets Shop</button></li>
              <li><button onClick={() => setCurrentTab('tracking')} className="hover:text-cyan-400">Track Cash on Delivery</button></li>
              <li><button onClick={() => setCurrentTab('db-schema')} className="hover:text-cyan-400">Database Schema Docs</button></li>
              <li><button onClick={() => setCurrentTab('admin')} className="hover:text-cyan-400">Store Management Admin</button></li>
            </ul>
          </div>

          <div>
            <h4 className="font-bold text-white text-sm mb-3">Customer Support</h4>
            <ul className="space-y-2">
              <li>Address: Commercial Market, Satellite Town, Rawalpindi, PK</li>
              <li>Phone / WhatsApp: +92 300 1234567</li>
              <li>Email: support@mkdigitalstore.pk</li>
              <li>Hours: Mon - Sat (10:00 AM - 10:00 PM)</li>
            </ul>
          </div>

          <div>
            <h4 className="font-bold text-white text-sm mb-3">Supported Payment Options</h4>
            <div className="flex flex-wrap gap-2 text-[10px] font-bold">
              <span className="bg-slate-950 border border-slate-800 px-3 py-1.5 rounded text-emerald-400">Cash on Delivery</span>
              <span className="bg-slate-950 border border-slate-800 px-3 py-1.5 rounded text-green-400">Easypaisa</span>
              <span className="bg-slate-950 border border-slate-800 px-3 py-1.5 rounded text-red-400">JazzCash</span>
              <span className="bg-slate-950 border border-slate-800 px-3 py-1.5 rounded text-cyan-400">Bank Transfer</span>
            </div>
          </div>
        </div>

        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-12 pt-6 border-t border-slate-800/80 text-center text-slate-500">
          © 2026 MK Digital Store Pakistan. All Rights Reserved. Designed for performance & speed.
        </div>
      </footer>
    </div>
  );
}


// Reusable Product Card Component
function ProductCard({ product, onSelect, onAddToCart, onToggleWishlist, isWishlisted, formatPKR }) {
  return (
    <div className="bg-slate-900 border border-slate-800 hover:border-cyan-500/40 rounded-2xl overflow-hidden flex flex-col justify-between group transition duration-300 hover:shadow-2xl hover:shadow-cyan-500/5">
      <div className="relative p-4 bg-slate-950/50 cursor-pointer overflow-hidden" onClick={() => onSelect(product.id)}>
        {/* Badges */}
        <div className="absolute top-3 left-3 flex flex-col gap-1 z-10">
          {product.discount && (
            <span className="bg-red-500 text-white font-bold text-[10px] px-2 py-0.5 rounded-full uppercase">
              -{product.discount}%
            </span>
          )}
          {product.isNew && (
            <span className="bg-cyan-500 text-slate-950 font-bold text-[10px] px-2 py-0.5 rounded-full uppercase">
              NEW
            </span>
          )}
        </div>

        {/* Wishlist Button */}
        <button
          onClick={(e) => { e.stopPropagation(); onToggleWishlist(product.id); }}
          className={`absolute top-3 right-3 p-2 rounded-full backdrop-blur-md z-10 transition ${isWishlisted ? 'bg-pink-500 text-white' : 'bg-slate-900/80 text-slate-400 hover:text-white'}`}
        >
          <Heart className="w-4 h-4 fill-current" />
        </button>

        <img 
          src={product.images[0]} 
          alt={product.name} 
          className="w-full h-48 object-contain transform group-hover:scale-105 transition duration-500 my-2" 
        />
      </div>

      <div className="p-5 flex-1 flex flex-col justify-between space-y-4">
        <div className="space-y-1">
          <span className="text-[11px] font-bold text-slate-500 uppercase tracking-wider">{product.category}</span>
          <h3 
            onClick={() => onSelect(product.id)} 
            className="font-bold text-sm text-slate-100 hover:text-cyan-400 transition cursor-pointer line-clamp-2"
          >
            {product.name}
          </h3>

          <div className="flex items-center space-x-1 text-amber-400 text-xs pt-1">
            <Star className="w-3.5 h-3.5 fill-amber-400" />
            <span className="font-bold text-slate-200">{product.rating}</span>
            <span className="text-slate-500 text-[11px]">({product.reviewsCount})</span>
          </div>
        </div>

        <div className="space-y-3 pt-2 border-t border-slate-800/80">
          <div className="flex items-baseline justify-between">
            <div>
              <span className="text-lg font-black text-cyan-400">{formatPKR(product.price)}</span>
              {product.originalPrice && (
                <span className="text-xs text-slate-500 line-through ml-2">{formatPKR(product.originalPrice)}</span>
              )}
            </div>
          </div>

          <button
            onClick={() => onAddToCart(product)}
            className="w-full bg-slate-800 hover:bg-cyan-500 hover:text-slate-950 text-white text-xs font-bold py-2.5 rounded-xl border border-slate-700 transition flex items-center justify-center space-x-2"
          >
            <ShoppingCart className="w-4 h-4" />
            <span>Add To Cart</span>
          </button>
        </div>
      </div>
    </div>
  );
}

// Multi-Image Gallery Component
function ProductImageGallery({ images, altText }) {
  const [activeImg, setActiveImg] = useState(images[0]);
  return (
    <div className="space-y-4">
      <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 h-96 flex items-center justify-center">
        <img src={activeImg} alt={altText} className="max-h-full max-w-full object-contain rounded-2xl" />
      </div>
      {images.length > 1 && (
        <div className="flex space-x-3 overflow-x-auto pb-2">
          {images.map((img, i) => (
            <img
              key={i}
              src={img}
              alt=""
              onClick={() => setActiveImg(img)}
              className={`w-20 h-20 object-cover rounded-xl bg-slate-900 border cursor-pointer transition ${activeImg === img ? 'border-cyan-500 ring-2 ring-cyan-500/30' : 'border-slate-800 opacity-60'}`}
            />
          ))}
        </div>
      )}
    </div>
  );
}

// Checkout View Component
function CheckoutView({ cart, cartGrandTotal, formatPKR, onOrderPlaced }) {
  const [paymentMethod, setPaymentMethod] = useState('COD');
  const [formData, setFormData] = useState({
    fullName: 'Hamza Khan',
    phone: '03001234567',
    email: 'hamza@example.pk',
    address: 'House 42, Street 10, F-11/1',
    city: 'Islamabad',
    province: 'Federal Capital'
  });

  const handleSubmit = (e) => {
    e.preventDefault();
    const newOrder = {
      id: `MK-${Math.floor(10000 + Math.random() * 90000)}`,
      date: new Date().toISOString().split('T')[0],
      items: cart,
      total: cartGrandTotal,
      paymentMethod: paymentMethod === 'COD' ? 'Cash on Delivery' : paymentMethod,
      status: 'Order Placed',
      customer: {
        name: formData.fullName,
        phone: formData.phone,
        email: formData.email,
        address: formData.address,
        city: formData.city,
        province: formData.province
      }
    };
    onOrderPlaced(newOrder);
  };

  return (
    <form onSubmit={handleSubmit} className="grid lg:grid-cols-3 gap-8">
      <div className="lg:col-span-2 space-y-6">
        
        {/* Customer Info Form */}
        <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 sm:p-8 space-y-4">
          <h3 className="font-bold text-white text-lg border-b border-slate-800 pb-3">1. Shipping & Contact Details</h3>
          
          <div className="grid sm:grid-cols-2 gap-4">
            <div>
              <label className="text-xs font-bold text-slate-400">Full Name *</label>
              <input
                required
                type="text"
                value={formData.fullName}
                onChange={e => setFormData({ ...formData, fullName: e.target.value })}
                className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
              />
            </div>
            <div>
              <label className="text-xs font-bold text-slate-400">WhatsApp / Mobile Number *</label>
              <input
                required
                type="text"
                value={formData.phone}
                onChange={e => setFormData({ ...formData, phone: e.target.value })}
                className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
              />
            </div>
          </div>

          <div>
            <label className="text-xs font-bold text-slate-400">Street Address *</label>
            <input
              required
              type="text"
              value={formData.address}
              onChange={e => setFormData({ ...formData, address: e.target.value })}
              className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
            />
          </div>

          <div className="grid sm:grid-cols-2 gap-4">
            <div>
              <label className="text-xs font-bold text-slate-400">City *</label>
              <select
                value={formData.city}
                onChange={e => setFormData({ ...formData, city: e.target.value })}
                className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
              >
                {PAKISTAN_CITIES.map((c, i) => (
                  <option key={i} value={c}>{c}</option>
                ))}
              </select>
            </div>
            <div>
              <label className="text-xs font-bold text-slate-400">Province</label>
              <input
                type="text"
                value={formData.province}
                onChange={e => setFormData({ ...formData, province: e.target.value })}
                className="w-full mt-1 bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-slate-200 focus:outline-none focus:border-cyan-500"
              />
            </div>
          </div>
        </div>

        {/* Payment Methods */}
        <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 sm:p-8 space-y-4">
          <h3 className="font-bold text-white text-lg border-b border-slate-800 pb-3">2. Choose Payment Method</h3>
          
          <div className="space-y-3">
            <label className={`flex items-center justify-between p-4 rounded-2xl border cursor-pointer transition ${paymentMethod === 'COD' ? 'bg-cyan-500/10 border-cyan-500' : 'bg-slate-950 border-slate-800'}`}>
              <div className="flex items-center space-x-3">
                <input type="radio" name="pay" checked={paymentMethod === 'COD'} onChange={() => setPaymentMethod('COD')} className="accent-cyan-500" />
                <div>
                  <div className="font-bold text-white text-sm">Cash on Delivery (COD)</div>
                  <div className="text-xs text-slate-400">Pay cash directly to courier rider upon doorstep delivery</div>
                </div>
              </div>
              <span className="text-xs font-bold text-emerald-400 bg-emerald-500/10 px-2.5 py-1 rounded-full">Recommended</span>
            </label>

            <label className={`flex items-center justify-between p-4 rounded-2xl border cursor-pointer transition ${paymentMethod === 'Easypaisa' ? 'bg-cyan-500/10 border-cyan-500' : 'bg-slate-950 border-slate-800'}`}>
              <div className="flex items-center space-x-3">
                <input type="radio" name="pay" checked={paymentMethod === 'Easypaisa'} onChange={() => setPaymentMethod('Easypaisa')} className="accent-cyan-500" />
                <div>
                  <div className="font-bold text-white text-sm">Easypaisa Mobile Wallet</div>
                  <div className="text-xs text-slate-400">Transfer payment to Easypaisa Account: 0300-1234567</div>
                </div>
              </div>
            </label>

            <label className={`flex items-center justify-between p-4 rounded-2xl border cursor-pointer transition ${paymentMethod === 'JazzCash' ? 'bg-cyan-500/10 border-cyan-500' : 'bg-slate-950 border-slate-800'}`}>
              <div className="flex items-center space-x-3">
                <input type="radio" name="pay" checked={paymentMethod === 'JazzCash'} onChange={() => setPaymentMethod('JazzCash')} className="accent-cyan-500" />
                <div>
                  <div className="font-bold text-white text-sm">JazzCash Mobile Wallet</div>
                  <div className="text-xs text-slate-400">Transfer payment to JazzCash Account: 0300-1234567</div>
                </div>
              </div>
            </label>
          </div>
        </div>

      </div>

      {/* Checkout Sidebar */}
      <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 h-fit space-y-6">
        <h3 className="font-bold text-white text-lg border-b border-slate-800 pb-3">Final Order Review</h3>
        
        <div className="space-y-3">
          {cart.map((item, idx) => (
            <div key={idx} className="flex justify-between text-xs text-slate-300">
              <span className="truncate max-w-[180px]">{item.qty}x {item.name}</span>
              <span className="font-bold">{formatPKR(item.price * item.qty)}</span>
            </div>
          ))}
        </div>

        <div className="border-t border-slate-800 pt-4 flex justify-between text-base font-black text-white">
          <span>Total Amount</span>
          <span className="text-cyan-400">{formatPKR(cartGrandTotal)}</span>
        </div>

        <button
          type="submit"
          className="w-full bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold py-4 rounded-xl shadow-xl transition"
        >
          Confirm & Place Order
        </button>
      </div>
    </form>
  );
}

// Admin Dashboard Component
function AdminDashboard({ products, orders, setProducts, setOrders, formatPKR, onViewDBSchema }) {
  const [adminTab, setAdminTab] = useState('overview'); // overview, products, orders, inventory

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 space-y-8">
      <div className="flex flex-col sm:flex-row justify-between items-start sm:items-center border-b border-slate-800 pb-6 gap-4">
        <div>
          <h1 className="text-3xl font-extrabold text-white flex items-center">
            <LayoutDashboard className="w-7 h-7 mr-3 text-cyan-400" /> Admin Control Dashboard
          </h1>
          <p className="text-slate-400 text-sm mt-1">Manage products, orders, stock inventory and database settings</p>
        </div>
        <button onClick={onViewDBSchema} className="bg-slate-800 hover:bg-slate-700 text-xs font-bold text-cyan-400 px-4 py-2.5 rounded-xl border border-slate-700 flex items-center">
          <Database className="w-4 h-4 mr-2" /> Inspect Database Schema
        </button>
      </div>

      {/* Admin Nav Tabs */}
      <div className="flex space-x-2 border-b border-slate-800 pb-2 overflow-x-auto">
        <button onClick={() => setAdminTab('overview')} className={`px-4 py-2 rounded-xl text-xs font-bold transition ${adminTab === 'overview' ? 'bg-cyan-500 text-slate-950' : 'text-slate-400 hover:text-white'}`}>
          Sales Overview
        </button>
        <button onClick={() => setAdminTab('products')} className={`px-4 py-2 rounded-xl text-xs font-bold transition ${adminTab === 'products' ? 'bg-cyan-500 text-slate-950' : 'text-slate-400 hover:text-white'}`}>
          Products CRUD ({products.length})
        </button>
        <button onClick={() => setAdminTab('orders')} className={`px-4 py-2 rounded-xl text-xs font-bold transition ${adminTab === 'orders' ? 'bg-cyan-500 text-slate-950' : 'text-slate-400 hover:text-white'}`}>
          Manage Orders ({orders.length})
        </button>
      </div>

      {/* Tab 1: Overview */}
      {adminTab === 'overview' && (
        <div className="space-y-8">
          <div className="grid grid-cols-2 md:grid-cols-4 gap-6">
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5">
              <span className="text-xs text-slate-400 font-bold uppercase">Total Revenue</span>
              <div className="text-2xl font-black text-cyan-400 mt-1">Rs. 485,200</div>
            </div>
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5">
              <span className="text-xs text-slate-400 font-bold uppercase">Total Orders</span>
              <div className="text-2xl font-black text-white mt-1">142</div>
            </div>
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5">
              <span className="text-xs text-slate-400 font-bold uppercase">Pending COD</span>
              <div className="text-2xl font-black text-amber-400 mt-1">18</div>
            </div>
            <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5">
              <span className="text-xs text-slate-400 font-bold uppercase">Low Stock Alerts</span>
              <div className="text-2xl font-black text-red-400 mt-1">2 Items</div>
            </div>
          </div>
        </div>
      )}

      {/* Tab 2: Product CRUD */}
      {adminTab === 'products' && (
        <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 space-y-4">
          <div className="flex justify-between items-center pb-4 border-b border-slate-800">
            <h3 className="font-bold text-white text-base">Store Catalog Items</h3>
            <button className="bg-cyan-500 text-slate-950 font-bold text-xs px-4 py-2 rounded-xl flex items-center">
              <Plus className="w-4 h-4 mr-1" /> Add New Product
            </button>
          </div>
          <div className="overflow-x-auto">
            <table className="w-full text-left text-xs text-slate-300">
              <thead className="bg-slate-950 text-slate-400 uppercase font-bold">
                <tr>
                  <th className="p-3">Product Name</th>
                  <th className="p-3">Category</th>
                  <th className="p-3">Price</th>
                  <th className="p-3">Stock Qty</th>
                  <th className="p-3">Actions</th>
                </tr>
              </thead>
              <tbody className="divide-y divide-slate-800">
                {products.map(p => (
                  <tr key={p.id}>
                    <td className="p-3 font-semibold text-white">{p.name}</td>
                    <td className="p-3 text-cyan-400">{p.category}</td>
                    <td className="p-3">{formatPKR(p.price)}</td>
                    <td className="p-3 font-bold">{p.stockQty} pcs</td>
                    <td className="p-3 space-x-2">
                      <button className="text-slate-400 hover:text-white">Edit</button>
                      <button className="text-red-400 hover:text-red-300">Delete</button>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      )}

      {/* Tab 3: Order Management */}
      {adminTab === 'orders' && (
        <div className="bg-slate-900 border border-slate-800 rounded-3xl p-6 space-y-4">
          <h3 className="font-bold text-white text-base border-b border-slate-800 pb-4">Customer Orders & Statuses</h3>
          <div className="overflow-x-auto">
            <table className="w-full text-left text-xs text-slate-300">
              <thead className="bg-slate-950 text-slate-400 uppercase font-bold">
                <tr>
                  <th className="p-3">Order ID</th>
                  <th className="p-3">Customer</th>
                  <th className="p-3">City</th>
                  <th className="p-3">Total Amount</th>
                  <th className="p-3">Status</th>
                  <th className="p-3">Update</th>
                </tr>
              </thead>
              <tbody className="divide-y divide-slate-800">
                {orders.map(o => (
                  <tr key={o.id}>
                    <td className="p-3 font-mono font-bold text-cyan-400">{o.id}</td>
                    <td className="p-3">{o.customer.name}</td>
                    <td className="p-3">{o.customer.city}</td>
                    <td className="p-3 font-bold text-white">{formatPKR(o.total)}</td>
                    <td className="p-3">
                      <span className="bg-cyan-500/10 text-cyan-400 px-2 py-0.5 rounded font-bold">{o.status}</span>
                    </td>
                    <td className="p-3">
                      <select 
                        value={o.status}
                        onChange={(e) => {
                          const updated = orders.map(ord => ord.id === o.id ? { ...ord, status: e.target.value } : ord);
                          setOrders(updated);
                        }}
                        className="bg-slate-950 border border-slate-800 text-slate-200 rounded p-1 text-[11px]"
                      >
                        <option value="Order Placed">Order Placed</option>
                        <option value="Processing">Processing</option>
                        <option value="Shipped">Shipped</option>
                        <option value="Delivered">Delivered</option>
                      </select>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      )}
    </div>
  );
}

// Database Schema Visualizer Component
function DatabaseSchemaView() {
  return (
    <div className="max-w-5xl mx-auto px-4 py-12 space-y-8">
      <div className="text-center space-y-2">
        <div className="inline-flex items-center space-x-2 bg-indigo-500/10 border border-indigo-500/30 px-3 py-1 rounded-full text-indigo-400 text-xs font-bold">
          <Database className="w-3.5 h-3.5" /> Backend Ready Relational Architecture
        </div>
        <h1 className="text-3xl font-extrabold text-white">PostgreSQL / MySQL Schema Reference</h1>
        <p className="text-slate-400 text-sm">Clean table declarations and relationships for developers connecting real databases</p>
      </div>

      <div className="grid md:grid-cols-2 gap-6">
        {[
          {
            tableName: 'users',
            schema: `CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  full_name VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  phone VARCHAR(50) NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role VARCHAR(20) DEFAULT 'customer',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);`
          },
          {
            tableName: 'products',
            schema: `CREATE TABLE products (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  slug VARCHAR(255) UNIQUE NOT NULL,
  category_id INT REFERENCES categories(id),
  price_pkr NUMERIC(10, 2) NOT NULL,
  original_price_pkr NUMERIC(10, 2),
  stock_quantity INT DEFAULT 0,
  is_featured BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);`
          },
          {
            tableName: 'orders',
            schema: `CREATE TABLE orders (
  id VARCHAR(50) PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  total_amount_pkr NUMERIC(10, 2) NOT NULL,
  payment_method VARCHAR(50) NOT NULL, -- 'COD', 'Easypaisa', 'JazzCash'
  order_status VARCHAR(50) DEFAULT 'Pending',
  courier_tracking_no VARCHAR(100),
  shipping_address TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);`
          },
          {
            tableName: 'order_items',
            schema: `CREATE TABLE order_items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  order_id VARCHAR(50) REFERENCES orders(id),
  product_id UUID REFERENCES products(id),
  quantity INT NOT NULL,
  unit_price_pkr NUMERIC(10, 2) NOT NULL,
  selected_variant VARCHAR(50)
);`
          }
        ].map((tbl, idx) => (
          <div key={idx} className="bg-slate-900 border border-slate-800 rounded-2xl p-5 space-y-3 font-mono">
            <div className="text-cyan-400 font-bold text-sm flex items-center justify-between border-b border-slate-800 pb-2">
              <span>Table: {tbl.tableName}</span>
              <span className="text-[10px] text-slate-500 font-sans">PostgreSQL</span>
            </div>
            <pre className="text-xs text-slate-300 overflow-x-auto leading-relaxed p-2 bg-slate-950 rounded-xl">
              {tbl.schema}
            </pre>
          </div>
        ))}
      </div>
    </div>
  );
}