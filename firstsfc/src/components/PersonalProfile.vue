<template>
  <div class="portfolio">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="nav-container">
        <div class="logo">JAYZEE</div>
        <button class="menu-toggle" @click="toggleMenu" aria-label="Toggle menu">
          <span></span>
          <span></span>
          <span></span>
        </button>
        <ul class="nav-menu" :class="{ active: isMenuOpen }">
          <li v-for="item in navItems" :key="item.id">
            <a :href="`#${item.id}`" class="nav-link" @click="closeMenu">{{ item.name }}</a>
          </li>
        </ul>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero-section">
      <div class="hero-content">
        <div class="profile-image-container">
          <img :src="profileImage" alt="Profile Picture" class="profile-image">
          <div class="image-glow"></div>
        </div>
        <h1 class="hero-title">{{ hero.title }}</h1>
        <p class="hero-subtitle">{{ hero.subtitle }}</p>
        <p class="hero-description">{{ hero.description }}</p>
        <div class="cta-buttons">
          <a href="#about" class="btn btn-primary">Explore My Work</a>
          <a href="#contact" class="btn btn-secondary">Get In Touch</a>
        </div>
      </div>
      <div class="scroll-indicator">
        <span></span>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
      <div class="container">
        <h2 class="section-title">About Me</h2>
        <div class="section-content">
          <div class="about-grid">
            <div class="about-text">
              <p v-for="(paragraph, index) in about.paragraphs" :key="index">
                {{ paragraph }}
              </p>
            </div>
            <div class="about-stats">
              <div v-for="stat in about.stats" :key="stat.label" class="stat-card">
                <div class="stat-number">{{ stat.number }}</div>
                <div class="stat-label">{{ stat.label }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- History Section -->
    <section id="history" class="section section-dark">
      <div class="container">
        <h2 class="section-title">Personal History</h2>
        <div class="section-content">
          <div class="timeline">
            <div v-for="item in timeline" :key="item.title" class="timeline-item">
              <div class="timeline-marker"></div>
              <div class="timeline-content">
                <h3>{{ item.title }}</h3>
                <h4>{{ item.subtitle }}</h4>
                <p>{{ item.description }}</p>
                <p v-if="item.detail" class="timeline-detail">{{ item.detail }}</p>
                <ul v-if="item.list" class="timeline-list">
                  <li v-for="listItem in item.list" :key="listItem">{{ listItem }}</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="section">
      <div class="container">
        <h2 class="section-title">Skills & Interests</h2>
        <div class="section-content">
          <div class="skills-grid">
            <div v-for="category in skills" :key="category.title" class="skill-category">
              <div class="skill-icon">{{ category.icon }}</div>
              <h3>{{ category.title }}</h3>
              <ul class="skill-list">
                <li v-for="skill in category.items" :key="skill">{{ skill }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section section-dark">
      <div class="container">
        <h2 class="section-title">Goals & Achievements</h2>
        <div class="section-content">
          <div class="goals-container">
            <div v-for="goal in goals" :key="goal.title" class="goal-card">
              <div class="goal-icon">{{ goal.icon }}</div>
              <h3>{{ goal.title }}</h3>
              <p>{{ goal.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section">
      <div class="container">
        <h2 class="section-title">Get In Touch</h2>
        <div class="section-content">
          <div class="contact-container">
            <div class="contact-info">
              <h3>Let's Connect</h3>
              <p>{{ contact.intro }}</p>
              <div class="contact-methods">
                <div v-for="method in contact.methods" :key="method.title" class="contact-method">
                  <div class="contact-icon">{{ method.icon }}</div>
                  <div class="contact-details">
                    <h4>{{ method.title }}</h4>
                    <p>{{ method.value }}</p>
                  </div>
                </div>
              </div>
            </div>
            <div class="contact-form">
              <form @submit.prevent="handleSubmit">
                <div class="form-group">
                  <input 
                    v-model="form.name" 
                    type="text" 
                    placeholder="Your Name" 
                    required
                  >
                </div>
                <div class="form-group">
                  <input 
                    v-model="form.email" 
                    type="email" 
                    placeholder="Your Email" 
                    required
                  >
                </div>
                <div class="form-group">
                  <textarea 
                    v-model="form.message" 
                    rows="5" 
                    placeholder="Your Message" 
                    required
                  ></textarea>
                </div>
                <button type="submit" class="btn btn-primary">Send Message</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Resources Section -->
    <section id="resources" class="section section-dark">
      <div class="container">
        <h2 class="section-title">Resources & Credits</h2>
        <div class="section-content">
          <div class="resources-grid">
            <div v-for="category in resources" :key="category.title" class="resource-category">
              <h3>{{ category.title }}</h3>
              <ul>
                <li v-for="item in category.items" :key="item.text">
                  <a v-if="item.link" :href="item.link" target="_blank" rel="noopener">
                    {{ item.text }}
                  </a>
                  <span v-else>{{ item.text }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <p>&copy; 2025 Jayzee. All rights reserved.</p>
        <p>Built with passion for technology and innovation</p>
      </div>
    </footer>
  </div>
</template>

<script>

import profileImage from '@/assets/Photo/Profile.svg'

export default {
  name: 'PersonalProfile',
  data() {
    return {
      isMenuOpen: false,
      profileImage,
      navItems: [
        { id: 'home', name: 'Home' },
        { id: 'about', name: 'About' },
        { id: 'history', name: 'History' },
        { id: 'skills', name: 'Skills' },
        { id: 'projects', name: 'Projects' },
        { id: 'contact', name: 'Contact' }
      ],
      hero: {
        title: 'Welcome to My Portfolio',
        subtitle: "I'm Jayzee",
        description: 'IT Student | Technology Enthusiast | Future Cybersecurity Specialist'
      },
      about: {
        paragraphs: [
          'I am someone who is deeply interested in technology, especially in how new innovations shape the future. I enjoy understanding how things work, from machine parts to computer systems, and I\'m constantly learning new skills that will help me grow in the IT field.',
          'My passion lies in cybersecurity and building innovative solutions. I believe in the power of technology to transform lives and create opportunities. With a strong foundation in IT and a drive to excel, I\'m working towards establishing my own firm specializing in cybersecurity.'
        ],
        stats: [
          { number: '2024', label: 'Graduate Year' },
          { number: 'BSIT', label: 'Current Course' },
          { number: '50%', label: 'Scholarship' }
        ]
      },
      timeline: [
        {
          title: 'Education',
          subtitle: 'National University MOA Campus',
          description: 'Graduated from Senior High School in Pasay City',
          detail: 'Awarded NU SHS Discount 2024 – 50% Tuition Scholarship (excluding miscellaneous fees)'
        },
        {
          title: 'Current Studies',
          subtitle: 'Bachelor of Science in Information Technology',
          description: 'Pursuing my passion for technology and cybersecurity',
          detail: 'Focusing on front-end and back-end development, computer systems, and security'
        },
        {
          title: 'IT Experience',
          subtitle: 'Practical Skills Development',
          description: 'Built hands-on experience through personal projects and gaming',
          list: [
            'Building and troubleshooting CPUs and desktop computers',
            'Basic front-end and back-end development',
            'Esports gaming on mobile and PC platforms'
          ]
        }
      ],
      skills: [
        {
          icon: '💻',
          title: 'Technical Skills',
          items: [
            'Computer Hardware Assembly & Troubleshooting',
            'Front-end Development (HTML, CSS, JavaScript)',
            'Back-end Development Basics',
            'Desktop Computer Systems',
            'Problem Solving & Critical Thinking'
          ]
        },
        {
          icon: '🎮',
          title: 'Gaming & Strategy',
          items: [
            'Esports Gaming (Mobile & PC)',
            'Chess & Strategy Games',
            'Team Coordination',
            'Quick Decision Making'
          ]
        },
        {
          icon: '🎯',
          title: 'Personal Interests',
          items: [
            'Understanding Machine Parts',
            'Technology Innovation',
            'Music (Various Genres)',
            'Walking & Physical Activity',
            'Continuous Learning'
          ]
        }
      ],
      goals: [
        {
          icon: '🔐',
          title: 'Cybersecurity Firm',
          description: 'Start an IT firm specializing in cybersecurity solutions and protecting digital assets'
        },
        {
          icon: '💼',
          title: 'Financial Freedom',
          description: 'Achieve sustainable financial independence where resources enable dreams and opportunities'
        },
        {
          icon: '❤️',
          title: 'Family & Community',
          description: 'Provide for the people I cherish and create positive impact in my community'
        },
        {
          icon: '🏆',
          title: 'Industry Recognition',
          description: 'Become a notable figure in the IT industry through innovation and excellence'
        },
        {
          icon: '🚀',
          title: 'Business Growth',
          description: 'Build and grow a successful company that creates value and employment opportunities'
        },
        {
          icon: '🎓',
          title: 'Scholarship Achievement',
          description: 'Received NU SHS 50% Tuition Scholarship for academic excellence'
        }
      ],
      contact: {
        intro: "I'm always open to discussing new opportunities, collaborations, or just having a conversation about technology and innovation.",
        methods: [
          { icon: '📧', title: 'Email', value: 'jzlopez@stuent.apc.edu.ph' },
          { icon: '📱', title: 'Phone', value: '+63 945 334 4925' },
          { icon: '📍', title: 'Location', value: 'Pasay City, Philippines' }
        ]
      },
      resources: [
        {
          title: 'Fonts',
          items: [
            { text: 'Orbitron - Google Fonts', link: 'https://fonts.google.com/specimen/Orbitron' },
            { text: 'Rajdhani - Google Fonts', link: 'https://fonts.google.com/specimen/Rajdhani' }
          ]
        },
        {
          title: 'Images',
          items: [
            { text: 'Profile Photo: Personal image owned by the developer' },
            { text: 'All images used are original and for educational purposes' }
          ]
        },
        {
          title: 'Development',
          items: [
            { text: 'HTML5, CSS3, JavaScript' },
            { text: 'Responsive Design Principles' },
            { text: 'AI-assisted code generation and optimization' },
            { text: 'Modern web development best practices' }
          ]
        },
        {
          title: 'AI Assistance',
          items: [
            { text: 'Development tools were used to assist in planning and refining code structure' },
            { text: 'Guided assistance supported layout, styling, and responsive design decisions' },
            { text: 'Final implementation, customization, and content by Jayzee' }
          ]
        }
      ],
      form: {
        name: '',
        email: '',
        message: ''
      }
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    closeMenu() {
      this.isMenuOpen = false
    },
    handleSubmit() {
      console.log('Form submitted:', this.form)
      alert('Thank you for your message! I will get back to you soon.')
      this.form = { name: '', email: '', message: '' }
    }
  }
}

</script>

<style>
</style>