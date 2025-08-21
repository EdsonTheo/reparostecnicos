import React, { useState } from 'react'
import { Button } from '@/components/ui/button.jsx'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card.jsx'
import { Badge } from '@/components/ui/badge.jsx'
import { 
  Smartphone, 
  Monitor, 
  Camera, 
  Tv, 
  Gamepad2, 
  Wrench, 
  MessageCircle, 
  ShoppingCart, 
  PlayCircle, 
  Star,
  Phone,
  Mail,
  MapPin,
  Clock,
  CheckCircle,
  Users,
  Award,
  Zap
} from 'lucide-react'
import './App.css'

function App() {
  const [activeService, setActiveService] = useState('computadores')
  const [chatOpen, setChatOpen] = useState(false)
  const [chatMessages, setChatMessages] = useState([
    { type: 'bot', message: 'Olá! Como posso ajudá-lo hoje?' },
  ])
  const [newMessage, setNewMessage] = useState('')
  const [formData, setFormData] = useState({
    nome: '',
    telefone: '',
    email: '',
    servico: '',
    descricao: ''
  })

  const services = {
    computadores: {
      title: 'Reparos de Computadores',
      description: 'Diagnóstico completo, limpeza, troca de componentes, formatação e otimização de performance.',
      icon: Monitor,
      image: '/src/assets/computer-repair.png',
      items: ['Formatação e reinstalação de SO', 'Troca de HD/SSD', 'Upgrade de memória RAM', 'Limpeza interna', 'Reparo de fonte']
    },
    celulares: {
      title: 'Reparos de Celulares',
      description: 'Troca de telas, baterias, conectores de carga, alto-falantes e reparo de placas.',
      icon: Smartphone,
      image: '/src/assets/phone-repair.png',
      items: ['Troca de tela', 'Substituição de bateria', 'Reparo de conector de carga', 'Troca de câmera', 'Desbloqueio']
    },
    cameras: {
      title: 'Câmeras de Vigilância',
      description: 'Instalação, configuração e manutenção de sistemas de monitoramento e segurança.',
      icon: Camera,
      image: '/src/assets/security-cameras.png',
      items: ['Instalação de câmeras', 'Configuração de DVR/NVR', 'Cabeamento estruturado', 'Acesso remoto', 'Manutenção preventiva']
    },
    televisores: {
      title: 'Reparos de Televisores',
      description: 'Conserto de TVs LED, LCD, OLED, Smart TVs e sistemas de áudio integrados.',
      icon: Tv,
      image: '/src/assets/tv-repair.png',
      items: ['Reparo de tela', 'Troca de placa principal', 'Configuração Smart TV', 'Reparo de áudio', 'Atualização de firmware']
    },
    videogames: {
      title: 'Reparos de Videogames',
      description: 'Manutenção e reparo de consoles PlayStation, Xbox, Nintendo e acessórios.',
      icon: Gamepad2,
      image: '/src/assets/hero-repair-tech.png',
      items: ['Limpeza interna', 'Troca de pasta térmica', 'Reparo de controles', 'Desbloqueio', 'Instalação de jogos']
    }
  }

  const testimonials = [
    {
      name: 'Maria Silva',
      rating: 5,
      comment: 'Excelente atendimento! Consertaram meu notebook em 2 dias. Recomendo!'
    },
    {
      name: 'João Santos',
      rating: 5,
      comment: 'Profissionais muito competentes. Instalaram câmeras de segurança na minha empresa.'
    },
    {
      name: 'Ana Costa',
      rating: 5,
      comment: 'Trocaram a tela do meu celular rapidamente e com garantia. Ótimo preço!'
    }
  ]

  const handleSendMessage = () => {
    if (newMessage.trim()) {
      setChatMessages([...chatMessages, { type: 'user', message: newMessage }])
      setNewMessage('')
      
      // Simular resposta automática
      setTimeout(() => {
        const responses = [
          'Obrigado pela sua mensagem! Um de nossos técnicos entrará em contato em breve.',
          'Posso ajudá-lo com informações sobre nossos serviços. Qual equipamento precisa de reparo?',
          'Nosso horário de atendimento é de segunda a sexta das 8h às 18h. Como posso ajudar?'
        ]
        const randomResponse = responses[Math.floor(Math.random() * responses.length)]
        setChatMessages(prev => [...prev, { type: 'bot', message: randomResponse }])
      }, 1000)
    }
  }

  const handleFormSubmit = (e) => {
    e.preventDefault()
    alert('Solicitação enviada com sucesso! Entraremos em contato em breve.')
    setFormData({
      nome: '',
      telefone: '',
      email: '',
      servico: '',
      descricao: ''
    })
  }

  const handleInputChange = (field, value) => {
    setFormData(prev => ({
      ...prev,
      [field]: value
    }))
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50">
      {/* Header */}
      <header className="bg-white shadow-lg sticky top-0 z-50">
        <div className="container mx-auto px-4 py-4">
          <div className="flex items-center justify-between">
            <div className="flex items-center space-x-2">
              <Wrench className="h-8 w-8 text-blue-600" />
              <h1 className="text-2xl font-bold text-gray-800">TechRepair Pro</h1>
            </div>
            <nav className="hidden md:flex space-x-6">
              <a href="#inicio" className="text-gray-600 hover:text-blue-600 transition-colors">Início</a>
              <a href="#servicos" className="text-gray-600 hover:text-blue-600 transition-colors">Serviços</a>
              <a href="#produtos" className="text-gray-600 hover:text-blue-600 transition-colors">Produtos</a>
              <a href="#tutoriais" className="text-gray-600 hover:text-blue-600 transition-colors">Tutoriais</a>
              <a href="#contato" className="text-gray-600 hover:text-blue-600 transition-colors">Contato</a>
            </nav>
            <div className="flex items-center space-x-4">
              <Button variant="outline" size="sm" onClick={() => setChatOpen(true)}>
                <MessageCircle className="h-4 w-4 mr-2" />
                Chat Online
              </Button>
              <Button size="sm">
                <Phone className="h-4 w-4 mr-2" />
                (11) 9999-9999
              </Button>
            </div>
          </div>
        </div>
      </header>

      {/* Hero Section */}
      <section id="inicio" className="py-20 bg-gradient-to-r from-blue-600 to-purple-700 text-white relative overflow-hidden">
        <div className="absolute inset-0 opacity-20">
          <img 
            src="/src/assets/hero-repair-tech.png" 
            alt="Oficina de reparos tecnológicos" 
            className="w-full h-full object-cover"
          />
        </div>
        <div className="container mx-auto px-4 text-center relative z-10">
          <h2 className="text-5xl font-bold mb-6">Assistência Técnica Especializada</h2>
          <p className="text-xl mb-8 max-w-3xl mx-auto">
            Reparos profissionais em computadores, celulares, câmeras de vigilância, televisores e videogames. 
            Atendimento rápido, qualidade garantida e preços justos.
          </p>
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <Button size="lg" className="bg-white text-blue-600 hover:bg-gray-100">
              <Wrench className="h-5 w-5 mr-2" />
              Solicitar Orçamento
            </Button>
            <Button size="lg" variant="outline" className="border-white text-white hover:bg-white hover:text-blue-600">
              <PlayCircle className="h-5 w-5 mr-2" />
              Ver Demonstração
            </Button>
          </div>
        </div>
      </section>

      {/* Stats Section */}
      <section className="py-16 bg-white">
        <div className="container mx-auto px-4">
          <div className="grid grid-cols-1 md:grid-cols-4 gap-8 text-center">
            <div className="flex flex-col items-center">
              <Users className="h-12 w-12 text-blue-600 mb-4" />
              <h3 className="text-3xl font-bold text-gray-800">5000+</h3>
              <p className="text-gray-600">Clientes Atendidos</p>
            </div>
            <div className="flex flex-col items-center">
              <Award className="h-12 w-12 text-blue-600 mb-4" />
              <h3 className="text-3xl font-bold text-gray-800">15+</h3>
              <p className="text-gray-600">Anos de Experiência</p>
            </div>
            <div className="flex flex-col items-center">
              <Zap className="h-12 w-12 text-blue-600 mb-4" />
              <h3 className="text-3xl font-bold text-gray-800">24h</h3>
              <p className="text-gray-600">Tempo Médio de Reparo</p>
            </div>
            <div className="flex flex-col items-center">
              <CheckCircle className="h-12 w-12 text-blue-600 mb-4" />
              <h3 className="text-3xl font-bold text-gray-800">98%</h3>
              <p className="text-gray-600">Taxa de Sucesso</p>
            </div>
          </div>
        </div>
      </section>

      {/* Services Section */}
      <section id="servicos" className="py-20 bg-gray-50">
        <div className="container mx-auto px-4">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-800 mb-4">Nossos Serviços</h2>
            <p className="text-xl text-gray-600 max-w-2xl mx-auto">
              Oferecemos soluções completas para todos os seus equipamentos eletrônicos
            </p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-5 gap-4 mb-8">
            {Object.entries(services).map(([key, service]) => {
              const Icon = service.icon
              return (
                <Button
                  key={key}
                  variant={activeService === key ? "default" : "outline"}
                  className="h-auto p-4 flex flex-col items-center space-y-2"
                  onClick={() => setActiveService(key)}
                >
                  <Icon className="h-8 w-8" />
                  <span className="text-sm font-medium">{service.title.split(' ')[2] || service.title.split(' ')[1]}</span>
                </Button>
              )
            })}
          </div>

          <Card className="max-w-4xl mx-auto">
            <CardHeader className="text-center">
              <div className="flex justify-center mb-4">
                <img 
                  src={services[activeService].image} 
                  alt={services[activeService].title}
                  className="w-32 h-32 object-contain rounded-lg"
                />
              </div>
              <CardTitle className="text-2xl">{services[activeService].title}</CardTitle>
              <CardDescription className="text-lg">{services[activeService].description}</CardDescription>
            </CardHeader>
            <CardContent>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                {services[activeService].items.map((item, index) => (
                  <div key={index} className="flex items-center space-x-2">
                    <CheckCircle className="h-5 w-5 text-green-500" />
                    <span>{item}</span>
                  </div>
                ))}
              </div>
              <div className="mt-6 text-center">
                <Button>Solicitar Orçamento para {services[activeService].title}</Button>
              </div>
            </CardContent>
          </Card>
        </div>
      </section>

      {/* Products Section */}
      <section id="produtos" className="py-20 bg-white">
        <div className="container mx-auto px-4">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-800 mb-4">Loja de Produtos</h2>
            <p className="text-xl text-gray-600">Peças originais e acessórios de qualidade</p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-4 gap-6">
            {[
              { name: 'Telas para Celular', price: 'A partir de R$ 89', category: 'Celulares' },
              { name: 'Baterias Originais', price: 'A partir de R$ 45', category: 'Celulares' },
              { name: 'SSD 480GB', price: 'R$ 189', category: 'Computadores' },
              { name: 'Memória RAM 8GB', price: 'R$ 159', category: 'Computadores' },
              { name: 'Câmera IP WiFi', price: 'R$ 299', category: 'Segurança' },
              { name: 'Controle PS5', price: 'R$ 349', category: 'Games' },
              { name: 'Cabo HDMI 4K', price: 'R$ 29', category: 'TV/Monitor' },
              { name: 'Fonte ATX 500W', price: 'R$ 179', category: 'Computadores' }
            ].map((product, index) => (
              <Card key={index} className="hover:shadow-lg transition-shadow">
                <CardContent className="p-4">
                  <div className="aspect-square bg-gray-100 rounded-lg mb-4 flex items-center justify-center">
                    <ShoppingCart className="h-12 w-12 text-gray-400" />
                  </div>
                  <Badge variant="secondary" className="mb-2">{product.category}</Badge>
                  <h3 className="font-semibold mb-2">{product.name}</h3>
                  <p className="text-lg font-bold text-blue-600 mb-3">{product.price}</p>
                  <Button size="sm" className="w-full">Comprar</Button>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Video Tutorials Section */}
      <section id="tutoriais" className="py-20 bg-gray-50">
        <div className="container mx-auto px-4">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-800 mb-4">Vídeo Tutoriais</h2>
            <p className="text-xl text-gray-600">Aprenda a resolver problemas básicos você mesmo</p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
            {[
              { title: 'Como Limpar seu Computador', duration: '8:45', views: '15K' },
              { title: 'Troca de Bateria do Celular', duration: '12:30', views: '23K' },
              { title: 'Configurar Câmera IP', duration: '15:20', views: '8K' },
              { title: 'Resolver Tela Azul Windows', duration: '10:15', views: '31K' },
              { title: 'Limpeza de Videogame', duration: '6:50', views: '12K' },
              { title: 'Conectar TV à Internet', duration: '9:30', views: '19K' }
            ].map((video, index) => (
              <Card key={index} className="hover:shadow-lg transition-shadow cursor-pointer">
                <CardContent className="p-0">
                  <div className="aspect-video bg-gray-800 rounded-t-lg relative flex items-center justify-center">
                    <PlayCircle className="h-16 w-16 text-white opacity-80" />
                    <div className="absolute bottom-2 right-2 bg-black bg-opacity-75 text-white text-xs px-2 py-1 rounded">
                      {video.duration}
                    </div>
                  </div>
                  <div className="p-4">
                    <h3 className="font-semibold mb-2">{video.title}</h3>
                    <p className="text-sm text-gray-600">{video.views} visualizações</p>
                  </div>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Testimonials */}
      <section className="py-20 bg-white">
        <div className="container mx-auto px-4">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-800 mb-4">O Que Nossos Clientes Dizem</h2>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
            {testimonials.map((testimonial, index) => (
              <Card key={index}>
                <CardContent className="p-6">
                  <div className="flex items-center mb-4">
                    {[...Array(testimonial.rating)].map((_, i) => (
                      <Star key={i} className="h-5 w-5 text-yellow-400 fill-current" />
                    ))}
                  </div>
                  <p className="text-gray-600 mb-4">"{testimonial.comment}"</p>
                  <p className="font-semibold">{testimonial.name}</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Contact Section */}
      <section id="contato" className="py-20 bg-blue-600 text-white">
        <div className="container mx-auto px-4">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold mb-4">Entre em Contato</h2>
            <p className="text-xl">Estamos prontos para ajudar você!</p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 gap-12">
            <div>
              <h3 className="text-2xl font-bold mb-6">Informações de Contato</h3>
              <div className="space-y-4">
                <div className="flex items-center space-x-3">
                  <Phone className="h-6 w-6" />
                  <span>(11) 9999-9999</span>
                </div>
                <div className="flex items-center space-x-3">
                  <Mail className="h-6 w-6" />
                  <span>contato@techrepairpro.com.br</span>
                </div>
                <div className="flex items-center space-x-3">
                  <MapPin className="h-6 w-6" />
                  <span>Rua da Tecnologia, 123 - São Paulo, SP</span>
                </div>
                <div className="flex items-center space-x-3">
                  <Clock className="h-6 w-6" />
                  <span>Seg-Sex: 8h às 18h | Sáb: 8h às 14h</span>
                </div>
              </div>

              <div className="mt-8">
                <h4 className="text-xl font-semibold mb-4">Suporte Online</h4>
                <div className="flex space-x-4">
                  <Button variant="outline" className="border-white text-white hover:bg-white hover:text-blue-600">
                    <MessageCircle className="h-4 w-4 mr-2" />
                    Chat ao Vivo
                  </Button>
                  <Button variant="outline" className="border-white text-white hover:bg-white hover:text-blue-600">
                    WhatsApp
                  </Button>
                </div>
              </div>
            </div>

            <div>
              <Card>
                <CardHeader>
                  <CardTitle className="text-gray-800">Solicitar Orçamento</CardTitle>
                  <CardDescription>Preencha o formulário e entraremos em contato</CardDescription>
                </CardHeader>
                <CardContent>
                  <form onSubmit={handleFormSubmit} className="space-y-4">
                    <div className="grid grid-cols-2 gap-4">
                      <div>
                        <label className="block text-sm font-medium text-gray-700 mb-1">Nome</label>
                        <input 
                          type="text" 
                          className="w-full p-2 border rounded-md" 
                          placeholder="Seu nome"
                          value={formData.nome}
                          onChange={(e) => handleInputChange('nome', e.target.value)}
                          required
                        />
                      </div>
                      <div>
                        <label className="block text-sm font-medium text-gray-700 mb-1">Telefone</label>
                        <input 
                          type="tel" 
                          className="w-full p-2 border rounded-md" 
                          placeholder="(11) 99999-9999"
                          value={formData.telefone}
                          onChange={(e) => handleInputChange('telefone', e.target.value)}
                          required
                        />
                      </div>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-1">Email</label>
                      <input 
                        type="email" 
                        className="w-full p-2 border rounded-md" 
                        placeholder="seu@email.com"
                        value={formData.email}
                        onChange={(e) => handleInputChange('email', e.target.value)}
                        required
                      />
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-1">Tipo de Serviço</label>
                      <select 
                        className="w-full p-2 border rounded-md"
                        value={formData.servico}
                        onChange={(e) => handleInputChange('servico', e.target.value)}
                        required
                      >
                        <option value="">Selecione o serviço</option>
                        <option value="computador">Reparo de Computador</option>
                        <option value="celular">Reparo de Celular</option>
                        <option value="cameras">Câmeras de Vigilância</option>
                        <option value="tv">Reparo de TV</option>
                        <option value="videogame">Reparo de Videogame</option>
                      </select>
                    </div>
                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-1">Descrição do Problema</label>
                      <textarea 
                        className="w-full p-2 border rounded-md h-24" 
                        placeholder="Descreva o problema..."
                        value={formData.descricao}
                        onChange={(e) => handleInputChange('descricao', e.target.value)}
                        required
                      ></textarea>
                    </div>
                    <Button type="submit" className="w-full">Enviar Solicitação</Button>
                  </form>
                </CardContent>
              </Card>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-800 text-white py-12">
        <div className="container mx-auto px-4">
          <div className="grid grid-cols-1 md:grid-cols-4 gap-8">
            <div>
              <div className="flex items-center space-x-2 mb-4">
                <Wrench className="h-6 w-6" />
                <h3 className="text-xl font-bold">TechRepair Pro</h3>
              </div>
              <p className="text-gray-400">
                Sua assistência técnica de confiança há mais de 15 anos.
              </p>
            </div>
            <div>
              <h4 className="font-semibold mb-4">Serviços</h4>
              <ul className="space-y-2 text-gray-400">
                <li>Reparo de Computadores</li>
                <li>Reparo de Celulares</li>
                <li>Câmeras de Vigilância</li>
                <li>Reparo de TVs</li>
                <li>Reparo de Videogames</li>
              </ul>
            </div>
            <div>
              <h4 className="font-semibold mb-4">Links Úteis</h4>
              <ul className="space-y-2 text-gray-400">
                <li>Garantia</li>
                <li>Política de Privacidade</li>
                <li>Termos de Uso</li>
                <li>FAQ</li>
                <li>Blog</li>
              </ul>
            </div>
            <div>
              <h4 className="font-semibold mb-4">Contato</h4>
              <ul className="space-y-2 text-gray-400">
                <li>(11) 9999-9999</li>
                <li>contato@techrepairpro.com.br</li>
                <li>Rua da Tecnologia, 123</li>
                <li>São Paulo, SP</li>
              </ul>
            </div>
          </div>
          <div className="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
            <p>&copy; 2024 TechRepair Pro. Todos os direitos reservados.</p>
          </div>
        </div>
      </footer>

      {/* Chat Online */}
      {chatOpen && (
        <div className="fixed bottom-4 right-4 w-80 h-96 bg-white rounded-lg shadow-2xl border z-50">
          <div className="bg-blue-600 text-white p-4 rounded-t-lg flex justify-between items-center">
            <h3 className="font-semibold">Chat Online - TechRepair Pro</h3>
            <button onClick={() => setChatOpen(false)} className="text-white hover:text-gray-200">
              ✕
            </button>
          </div>
          <div className="h-64 overflow-y-auto p-4 space-y-2">
            {chatMessages.map((msg, index) => (
              <div key={index} className={`flex ${msg.type === 'user' ? 'justify-end' : 'justify-start'}`}>
                <div className={`max-w-xs p-2 rounded-lg ${
                  msg.type === 'user' 
                    ? 'bg-blue-600 text-white' 
                    : 'bg-gray-200 text-gray-800'
                }`}>
                  {msg.message}
                </div>
              </div>
            ))}
          </div>
          <div className="p-4 border-t">
            <div className="flex space-x-2">
              <input
                type="text"
                value={newMessage}
                onChange={(e) => setNewMessage(e.target.value)}
                onKeyPress={(e) => e.key === 'Enter' && handleSendMessage()}
                placeholder="Digite sua mensagem..."
                className="flex-1 p-2 border rounded-md text-sm"
              />
              <Button size="sm" onClick={handleSendMessage}>
                Enviar
              </Button>
            </div>
          </div>
        </div>
      )}
    </div>
  )
}

export default App
