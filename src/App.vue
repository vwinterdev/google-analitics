<script setup lang="ts">
import { ref, onMounted } from 'vue'

const isScrolled = ref(false)
const activeSection = ref('hero')

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  updateActiveSection()
}

const updateActiveSection = () => {
  const sections = ['hero', 'about', 'services', 'contact']
  const scrollPosition = window.scrollY + 100

  for (const section of sections) {
    const element = document.getElementById(section)
    if (element) {
      const offsetTop = element.offsetTop
      const offsetHeight = element.offsetHeight
      if (scrollPosition >= offsetTop && scrollPosition < offsetTop + offsetHeight) {
        activeSection.value = section
        break
      }
    }
  }
}

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleSubmit = (e: Event) => {
  e.preventDefault()
  alert('Спасибо за ваше сообщение! Мы свяжемся с вами в ближайшее время.')
  const form = e.target as HTMLFormElement
  form.reset()
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll()
})
</script>

<template>
  <div class="app">
    <!-- Navigation -->
    <nav :class="{ scrolled: isScrolled }">
      <div class="nav-container">
        <div class="logo" @click="scrollToSection('hero')">
          <span>YourBrand</span>
        </div>
        <ul class="nav-links">
          <li>
            <a 
              :class="{ active: activeSection === 'hero' }"
              @click.prevent="scrollToSection('hero')"
            >
              Главная
            </a>
          </li>
          <li>
            <a 
              :class="{ active: activeSection === 'about' }"
              @click.prevent="scrollToSection('about')"
            >
              О нас
            </a>
          </li>
          <li>
            <a 
              :class="{ active: activeSection === 'services' }"
              @click.prevent="scrollToSection('services')"
            >
              Услуги
            </a>
          </li>
          <li>
            <a 
              :class="{ active: activeSection === 'contact' }"
              @click.prevent="scrollToSection('contact')"
            >
              Контакты
            </a>
          </li>
        </ul>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="hero" class="hero">
      <div class="hero-content">
        <h1 class="hero-title">
          <span class="gradient-text">Добро пожаловать</span>
          <br />
          в будущее
        </h1>
        <p class="hero-subtitle">
          Мы создаем инновационные решения для вашего бизнеса
        </p>
        <div class="hero-buttons">
          <button class="btn btn-primary" @click="scrollToSection('contact')">
            Начать
          </button>
          <button class="btn btn-secondary" @click="scrollToSection('about')">
            Узнать больше
          </button>
        </div>
      </div>
      <div class="hero-background">
        <div class="gradient-orb orb-1"></div>
        <div class="gradient-orb orb-2"></div>
        <div class="gradient-orb orb-3"></div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about">
      <div class="container">
        <h2 class="section-title">О нас</h2>
        <div class="about-content">
          <div class="about-text">
            <p>
              Мы команда профессионалов, специализирующихся на создании
              современных веб-решений и цифровых продуктов.
            </p>
            <p>
              Наш опыт и креативный подход помогают клиентам достигать
              выдающихся результатов в цифровом пространстве.
            </p>
          </div>
          <div class="stats">
            <div class="stat-item">
              <div class="stat-number">500+</div>
              <div class="stat-label">Проектов</div>
            </div>
            <div class="stat-item">
              <div class="stat-number">200+</div>
              <div class="stat-label">Клиентов</div>
            </div>
            <div class="stat-item">
              <div class="stat-number">10+</div>
              <div class="stat-label">Лет опыта</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section id="services" class="services">
      <div class="container">
        <h2 class="section-title">Наши услуги</h2>
        <div class="services-grid">
          <div class="service-card">
            <div class="service-icon">🚀</div>
            <h3>Веб-разработка</h3>
            <p>
              Создание современных, быстрых и адаптивных веб-приложений
              с использованием передовых технологий.
            </p>
          </div>
          <div class="service-card">
            <div class="service-icon">📱</div>
            <h3>Мобильные приложения</h3>
            <p>
              Разработка нативных и кроссплатформенных мобильных
              приложений для iOS и Android.
            </p>
          </div>
          <div class="service-card">
            <div class="service-icon">🎨</div>
            <h3>UI/UX дизайн</h3>
            <p>
              Создание интуитивных и красивых интерфейсов, которые
              обеспечивают отличный пользовательский опыт.
            </p>
          </div>
          <div class="service-card">
            <div class="service-icon">⚡</div>
            <h3>Оптимизация</h3>
            <p>
              Повышение производительности и скорости работы ваших
              приложений для лучшего пользовательского опыта.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
      <div class="container">
        <h2 class="section-title">Свяжитесь с нами</h2>
        <div class="contact-content">
          <div class="contact-info">
            <h3>Давайте обсудим ваш проект</h3>
            <p>
              Мы всегда готовы ответить на ваши вопросы и обсудить
              возможности сотрудничества.
            </p>
            <div class="contact-details">
              <div class="contact-item">
                <span class="contact-icon">📧</span>
                <span>info@example.com</span>
              </div>
              <div class="contact-item">
                <span class="contact-icon">📞</span>
                <span>+7 (999) 123-45-67</span>
              </div>
              <div class="contact-item">
                <span class="contact-icon">📍</span>
                <span>Москва, Россия</span>
              </div>
            </div>
          </div>
          <form class="contact-form" @submit.prevent="handleSubmit">
            <div class="form-group">
              <input type="text" placeholder="Ваше имя" required />
            </div>
            <div class="form-group">
              <input type="email" placeholder="Email" required />
            </div>
            <div class="form-group">
              <textarea placeholder="Сообщение" rows="5" required></textarea>
            </div>
            <button type="submit" class="btn btn-primary">Отправить</button>
          </form>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <p>&copy; 2024 YourBrand. Все права защищены.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
}

/* Navigation */
nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(18, 18, 18, 0.8);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
  border-bottom: 1px solid transparent;
}

nav.scrolled {
  background: rgba(18, 18, 18, 0.95);
  border-bottom-color: rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.05);
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
  cursor: pointer;
}

.nav-links a:hover,
.nav-links a.active {
  color: #fff;
}

.nav-links a.active::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Hero Section */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  padding-top: 80px;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
  overflow: hidden;
}

.gradient-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.5;
  animation: float 20s infinite ease-in-out;
}

.orb-1 {
  width: 500px;
  height: 500px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  top: -200px;
  left: -200px;
  animation-delay: 0s;
}

.orb-2 {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  bottom: -150px;
  right: -150px;
  animation-delay: 5s;
}

.orb-3 {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation-delay: 10s;
}

@keyframes float {
  0%, 100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(30px, -30px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }
}

.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
  max-width: 800px;
  padding: 2rem;
}

.hero-title {
  font-size: clamp(2.5rem, 8vw, 5rem);
  font-weight: 800;
  line-height: 1.2;
  margin-bottom: 1.5rem;
  color: #fff;
}

.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: clamp(1rem, 2vw, 1.5rem);
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 2.5rem;
  line-height: 1.6;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  padding: 1rem 2.5rem;
  font-size: 1.1rem;
  font-weight: 600;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: inherit;
}

.btn-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: #fff;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 15px 40px rgba(102, 126, 234, 0.6);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.1);
  color: #fff;
  border: 2px solid rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
}

/* Container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

/* Section Styles */
section {
  padding: 6rem 0;
  position: relative;
}

.section-title {
  font-size: clamp(2rem, 5vw, 3.5rem);
  font-weight: 700;
  text-align: center;
  margin-bottom: 4rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* About Section */
.about {
  background: #1a1a1a;
  color: #fff;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.about-text p {
  font-size: 1.2rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 1.5rem;
}

.stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.stat-item {
  text-align: center;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.3s ease;
}

.stat-item:hover {
  transform: translateY(-5px);
  background: rgba(255, 255, 255, 0.08);
}

.stat-number {
  font-size: 3rem;
  font-weight: 800;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.stat-label {
  color: rgba(255, 255, 255, 0.7);
  font-size: 1.1rem;
}

/* Services Section */
.services {
  background: #121212;
  color: #fff;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.service-card {
  padding: 2.5rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  text-align: center;
}

.service-card:hover {
  transform: translateY(-10px);
  background: rgba(255, 255, 255, 0.08);
  border-color: rgba(102, 126, 234, 0.5);
  box-shadow: 0 20px 40px rgba(102, 126, 234, 0.2);
}

.service-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
}

.service-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #fff;
}

.service-card p {
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.6;
}

/* Contact Section */
.contact {
  background: #1a1a1a;
  color: #fff;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.contact-info h3 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.contact-info p {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.8;
  margin-bottom: 2rem;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  color: rgba(255, 255, 255, 0.8);
}

.contact-icon {
  font-size: 1.5rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  color: #fff;
  font-family: inherit;
  font-size: 1rem;
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
  background: rgba(255, 255, 255, 0.08);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

/* Footer */
.footer {
  background: #0a0a0a;
  color: rgba(255, 255, 255, 0.6);
  text-align: center;
  padding: 2rem 0;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

/* Responsive */
@media (max-width: 768px) {
  .nav-links {
    gap: 1rem;
    font-size: 0.9rem;
  }

  .about-content,
  .contact-content {
    grid-template-columns: 1fr;
  }

  .stats {
    grid-template-columns: 1fr;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }

  .hero-buttons {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}
</style>
