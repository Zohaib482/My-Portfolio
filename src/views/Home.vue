<script setup lang="ts">
import { onMounted, reactive, ref, computed } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { ScrollToPlugin } from 'gsap/ScrollToPlugin'
import SectionAmbientBg from '../components/SectionAmbientBg.vue'

// Register GSAP plugins
gsap.registerPlugin(ScrollTrigger, ScrollToPlugin)

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const activeFilter = ref('all')
const isMenuOpen = ref(false)
const scrollY = ref(0)

const projects = ref([
  {
    id: 1,
    title: 'Laravel RBAC Package',
    category: 'package',
    description: 'Role-Based Access Control package for Laravel with built-in authentication and email verification support. Open source package with comprehensive documentation.',
    image: 'RBAC',
    tags: ['Laravel Package', 'Authentication', 'Role Management'],
    technologies: ['PHP', 'Laravel', 'Composer', 'PHPUnit'],
    duration: '2 months',
    teamSize: '1 member',
    impact: 'Open Source Package',
    budget: 'Open Source',
    role: 'Lead Developer',
    link: 'https://github.com/Zohaib482/laravel-simple-rbac'
  },
  {
    id: 2,
    title: 'Countryroof CRM',
    category: 'crm',
    description: 'Customer Relationship Management system developed in Laravel and Livewire with real-time updates and comprehensive client management features.',
    image: 'CRM',
    tags: ['CRM', 'Laravel', 'Livewire', 'Real-time'],
    technologies: ['PHP', 'Laravel', 'Livewire', 'MySQL', 'JavaScript'],
    duration: '4 months',
    teamSize: '3 members',
    impact: 'Business Operations',
    budget: '$15K',
    role: 'Lead Developer',
    link: 'https://countryroof.com'
  },
  {
    id: 3,
    title: 'Ministry of Travel',
    category: 'travel',
    description: 'Travel Management and Flight booking application with real-time flight data integration, booking management, and payment processing.',
    image: 'TRAVEL',
    tags: ['Travel Booking', 'Flight Integration', 'Payment Gateway'],
    technologies: ['PHP', 'Laravel', 'MySQL', 'API Integration', 'Payment Gateway'],
    duration: '6 months',
    teamSize: '4 members',
    impact: 'Travel Industry',
    budget: '$25K',
    role: 'Senior Developer',
    link: 'https://ministryoftravel.com.au'
  },
  {
    id: 4,
    title: 'Last Minute Cleaning',
    category: 'cleaning',
    description: 'CRM project with Twilio conference call integration, real-time notifications through Websockets, and comprehensive service management.',
    image: 'CLEAN',
    tags: ['CRM', 'Twilio Integration', 'Websockets', 'Real-time'],
    technologies: ['PHP', 'Laravel', 'Twilio API', 'Websockets', 'MySQL'],
    duration: '5 months',
    teamSize: '3 members',
    impact: 'Service Industry',
    budget: '$20K',
    role: 'Lead Developer',
    link: 'https://lastminutecleaning.com.au'
  },
  {
    id: 5,
    title: 'IoT Architecture System',
    category: 'iot',
    description: 'IoT architecture design for connected systems integrating physical devices with digital platforms, featuring sensor data collection and processing.',
    image: 'IOT',
    tags: ['IoT', 'Architecture', 'Sensor Integration', 'Data Processing'],
    technologies: ['Python', 'Arduino', 'MQTT', 'Node.js', 'MongoDB'],
    duration: '3 months',
    teamSize: '2 members',
    impact: 'IoT Innovation',
    budget: '$12K',
    role: 'IoT Architect'
  },
  {
    id: 6,
    title: 'Custom Web Applications',
    category: 'web',
    description: 'Multiple custom web applications for desktop and mobile operating systems with responsive design and modern frameworks.',
    image: 'WEB',
    tags: ['Web Development', 'Mobile Friendly', 'Responsive Design'],
    technologies: ['HTML5', 'CSS3', 'JavaScript', 'PHP', 'Laravel', 'Vue.js'],
    duration: 'Ongoing',
    teamSize: '2-5 members',
    impact: 'Multiple Industries',
    budget: 'Variable',
    role: 'Full Stack Developer'
  }
])

const skills = [
  { 
    category: 'Back-end Development', 
    items: ['PHP 7/8', 'Laravel', 'CodeIgniter 3/4', 'Livewire', 'Django (Basics)', 'ASP.NET(MVC)', 'MySQL', 'SQL'], 
    level: 95 
  },
  { 
    category: 'Front-end Development', 
    items: ['HTML5', 'CSS3', 'JavaScript', 'jQuery', 'Vue.js', 'ReactJS', 'Flutter/Dart'], 
    level: 90 
  },
  { 
    category: 'Project Management', 
    items: ['Stakeholder Management', 'Project Planning & Execution', 'Team Leadership', 'Agile Methodologies', 'Jira', 'Trello'], 
    level: 88 
  },
  { 
    category: 'Technical Skills', 
    items: ['Technical Analysis', 'Software Best Practices', 'IoT Architect', 'Ability to learn new technologies'], 
    level: 92 
  }
]

const experience = [
  {
    title: 'Senior Web Developer',
    company: '360 Tech Solution',
    period: 'Nov 2021 - Present',
    location: 'Karachi, Sindh',
    achievements: [
      'Led end-to-end website and web application projects, managing scope, timelines, resources, and cross-functional teams',
      'Planned and oversaw website development lifecycle, converting client mockups into functional web presences',
      'Coordinated front-end and back-end development using HTML5, CSS3, PHP/Laravel, and related technologies',
      'Managed debugging, quality assurance, and pre-launch testing to ensure high-quality deployments',
      'Transitioned legacy websites to modern, user-friendly versions while integrating new features',
      'Served as primary point of contact for clients, gathering requirements and resolving issues post-launch',
      'Directed back-end architecture using PHP/Laravel with security patching and compliance standards',
      'Handled multi-project multitasking, deadline management, and end-user training on CMS/security'
    ],
    technologies: ['PHP', 'Laravel', 'Livewire', 'MySQL', 'JavaScript', 'Vue.js', 'AJAX', 'JSON'],
    responsibilities: ['Project Management', 'Client Communication', 'Back-end Architecture', 'Quality Assurance', 'Team Leadership']
  },
  {
    title: 'Visiting Faculty',
    company: 'APTECH Computer Education',
    period: 'Jan 2024 - Present',
    location: 'Metro Star Gate, Karachi, Sindh',
    achievements: [
      'Educated and trained students in web development principles and programming languages',
      'Designed and delivered lectures on web technologies including Laravel and back-end frameworks',
      'Mentored students on projects and assignments, providing constructive feedback',
      'Created curriculum and course materials aligned with current industry standards'
    ],
    technologies: ['PHP', 'Laravel', 'Web Development', 'Programming Fundamentals'],
    responsibilities: ['Teaching', 'Curriculum Development', 'Student Mentoring', 'Project Guidance']
  },
  {
    title: 'Web Developer, Team Lead',
    company: 'Deevloopers',
    period: 'Feb 2020 - Oct 2021',
    location: 'Karachi, Sindh',
    achievements: [
      'Collaborated with Developers to select ambitious coding milestones for software projects',
      'Updated old code bases to modern development standards, improving functionality',
      'Planned and developed interfaces that simplified overall management and ease of use',
      'Integrated constructive programs into cohesive product solutions',
      'Participated in software field testing to verify performance of developed projects',
      'Introduced agile methodologies and development best practices to enhance product development',
      'Designed intuitive graphical user interfaces to improve user experience',
      'Collaborated on systems development lifecycle from requirement gathering to production'
    ],
    technologies: ['PHP', 'JavaScript', 'MySQL', 'Agile', 'Code Review', 'UI/UX Design'],
    responsibilities: ['Team Leadership', 'Code Development', 'Agile Implementation', 'UI Design', 'Quality Assurance']
  }
]

const education = [
  {
    degree: 'Bachelor of Science in Computer Science',
    institution: 'Preston University',
    period: '2020',
    location: 'Karachi'
  },
  {
    degree: 'Higher Secondary School Certificate in Computer Science',
    institution: 'Board of Intermediate Education',
    period: '2015',
    location: 'Karachi'
  },
  {
    degree: 'Secondary School Certificate in Computer Science',
    institution: 'Falcon House Grammar School',
    period: '2013',
    location: 'Karachi'
  }
]

const hobbies = [
  { name: 'Gym Workout', icon: 'fas fa-dumbbell' },
  { name: 'ESports', icon: 'fas fa-gamepad' },
  { name: 'Internet Browsing', icon: 'fas fa-globe' }
]

const filteredProjects = computed(() => {
  const currentFilter = activeFilter.value
  const allProjects = projects.value

  if (currentFilter == 'all') {
    return allProjects
  } else {
    return allProjects.filter(project => project.category == currentFilter)
  }
})

// Mouse glow effect (still using reactive for the glow follower)
const mouseX = ref(0)
const mouseY = ref(0)

const mouseGlowStyle = computed(() => ({
  left: mouseX.value + 'px',
  top: mouseY.value + 'px'
}))

window.addEventListener('mousemove', (e) => {
  mouseX.value = e.clientX
  mouseY.value = e.clientY
})

onMounted(() => {
  // --- HERO ANIMATIONS ---
  const heroTl = gsap.timeline({ defaults: { ease: 'power4.out', duration: 0.8 } })
  
  heroTl.from('.hero-badge', { y: -50, opacity: 0, delay: 0.5 })
    .from('.hero-title', { y: 100, opacity: 0, scale: 0.9 }, '-=0.8')
    .from('.hero-subtitle', { y: 30, opacity: 0 }, '-=0.8')
    .from('.hero-description', { y: 20, opacity: 0 }, '-=0.8')
    .from('.hero-stats .stat', { y: 20, opacity: 0, stagger: 0.2 }, '-=0.8')
    .from('.hero-buttons', { y: 20, opacity: 0 }, '-=0.8')
    .fromTo('.profile-card', 
      { 
        x: 100, 
        autoAlpha: 0, 
        rotate: 5, 
        scale: 0.9 
      },
      {
        x: 0,
        autoAlpha: 1,
        rotate: 0,
        scale: 1,
        duration: .5,
        ease: 'power3.out',
        onComplete: () => {
          gsap.to('.profile-card', {
            y: -20,
            duration: .5,
            repeat: -1,
            yoyo: true,
            ease: 'power1.inOut'
          })
        }
      }, 
    '-=1.2')

  // --- SECTION ENTRANCE ANIMATIONS ---
  const sections = document.querySelectorAll('.section')
  sections.forEach(section => {
    const title = section.querySelector('.section-title')
    const subtitle = section.querySelector('.section-subtitle')
    
    if (title) {
      gsap.from(title, {
        scrollTrigger: {
          trigger: title,
          start: 'top 85%',
          toggleActions: 'play none none none'
        },
        y: 50,
        opacity: 0,
        duration: 1,
        ease: 'power3.out'
      })
    }
    
    if (subtitle) {
      gsap.from(subtitle, {
        scrollTrigger: {
          trigger: subtitle,
          start: 'top 85%',
          toggleActions: 'play none none none'
        },
        y: 30,
        opacity: 0,
        duration: 1,
        delay: 0.2,
        ease: 'power3.out'
      })
    }
  })

  // --- SKILLS ANIMATIONS ---
  gsap.from('.skill-category', {
    scrollTrigger: {
      trigger: '.skills-grid',
      start: 'top 80%',
    },
    y: 60,
    opacity: 0,
    stagger: 0.15,
    duration: 1,
    ease: 'back.out(1.7)',
    immediateRender: false
  })

  // Skill bars progress animation
  document.querySelectorAll('.skill-item').forEach(item => {
    const fill = item.querySelector('.progress-fill')
    if (fill) {
      const targetWidth = (fill as HTMLElement).getAttribute('data-level') + '%'
      gsap.set(fill, { width: 0 })
      
      gsap.to(fill, {
        scrollTrigger: {
          trigger: item,
          start: 'top 90%',
        },
        width: (fill as HTMLElement).dataset.width || targetWidth,
        duration: 1.5,
        ease: 'power2.out',
        delay: 0.3
      })
    }
  })

  // --- EXPERIENCE TIMELINE ANIMATIONS ---
  document.querySelectorAll('.timeline-item').forEach((item, index) => {
    const isLeft = item.classList.contains('fade-in-left')
    gsap.from(item, {
      scrollTrigger: {
        trigger: item,
        start: 'top 85%',
      },
      x: isLeft ? -100 : 100,
      opacity: 0,
      duration: 1.2,
      ease: 'power3.out',
      immediateRender: false
    })
  })

  // --- PROJECTS GRID ANIMATIONS ---
  const setupProjectAnimations = () => {
    gsap.from('.project-card', {
      scrollTrigger: {
        trigger: '.projects-grid',
        start: 'top 80%',
      },
      scale: 0.9,
      y: 50,
      opacity: 0,
      stagger: 0.1,
      duration: 0.8,
      ease: 'power2.out',
      clearProps: 'all',
      immediateRender: false
    })
  }
  setupProjectAnimations()

  // --- PARALLAX EFFECTS ---
  gsap.to('.hero-background', {
    scrollTrigger: {
      trigger: '.hero',
      start: 'top top',
      end: 'bottom top',
      scrub: true
    },
    y: 200,
    ease: 'none'
  })

  // --- CUSTOM CURSOR ---
  const cursorInner = document.querySelector('.cursor-inner')
  const cursorOuter = document.querySelector('.cursor-outer')

  if (cursorInner && cursorOuter) {
    // Hide default cursor on body
    document.body.style.cursor = 'none'

    // Set initial centering using percent to avoid GSAP overwriting it later
    gsap.set([cursorInner, cursorOuter], { xPercent: -50, yPercent: -50 })

    window.addEventListener('mousemove', (e) => {
      // Direct move for inner dot (zero duration for instant tracking)
      gsap.to(cursorInner, {
        x: e.clientX,
        y: e.clientY,
        duration: 0.05,
        ease: 'power2.out'
      })
      // Smooth follow for outer circle
      gsap.to(cursorOuter, {
        x: e.clientX,
        y: e.clientY,
        duration: 0.4,
        ease: 'power2.out'
      })
    })

    // Interactions
    const interactiveElements = 'a, button, .hover-lift, .project-card, .filter-btn, .stat'
    document.querySelectorAll(interactiveElements).forEach(el => {
      el.addEventListener('mouseenter', () => {
        gsap.to(cursorInner, { scale: 1.5, backgroundColor: 'var(--accent-color)' })
        gsap.to(cursorOuter, { scale: 1.2, borderColor: 'var(--accent-color)', opacity: 0.3, backgroundColor: 'var(--accent-color)' })
      })
      el.addEventListener('mouseleave', () => {
        gsap.to(cursorInner, { scale: 1, backgroundColor: 'white' })
        gsap.to(cursorOuter, { scale: 1, borderColor: 'white', opacity: 1, backgroundColor: 'transparent' })
      })
    })
  }

  // Refresh ScrollTrigger to ensure all heights are calculated
  setTimeout(() => {
    ScrollTrigger.refresh()
  }, 1000)
})

const submitForm = () => {
  alert('Thank you for your message! I will get back to you soon.')
  form.name = ''
  form.email = ''
  form.subject = ''
  form.message = ''
}

const triggerProjectAnimations = () => {
  gsap.from('.project-card', {
    scale: 0.9,
    y: 30,
    opacity: 0,
    stagger: 0.05,
    duration: 0.6,
    ease: 'power2.out',
    clearProps: 'all'
  })
}

const setActiveFilter = (filter: string) => {
  activeFilter.value = filter
  setTimeout(triggerProjectAnimations, 50)
}

const toggleMobileMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
  <div class="home">
    <!-- Custom Cursor -->
    <div class="custom-cursor-container">
      <div class="cursor-inner"></div>
      <div class="cursor-outer"></div>
    </div>
    
    <!-- Mouse Glow Effect -->
    <div class="mouse-glow" :style="mouseGlowStyle"></div>
    
    <!-- Interactive Background -->
    <div class="interactive-bg"></div>
    
    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="hero-background parallax">
        <div class="hero-particles float-element"></div>
        <div class="hero-gradient"></div>
        <div class="floating-shapes">
          <div class="shape shape-1 float-element"></div>
          <div class="shape shape-2 float-element"></div>
          <div class="shape shape-3 float-element"></div>
        </div>
      </div>
      <div class="container">
        <div class="hero-content">
          <div class="hero-text">
            <div class="hero-badge fade-in-up">
              <i class="fas fa-circle-check status-icon"></i>
              Available for Opportunities
            </div>
            <h1 class="hero-title fade-in">
              Hi, I'm <span class="hero-name-gradient">Zohaib Khan</span>
            </h1>
            <h2 class="hero-subtitle fade-in-up">Senior Web Developer & Technical Project Manager</h2>
            <p class="hero-description fade-in">
              Tech-savvy Web Development professional with strong expertise in Back-end development and Technical Project Management. Specialized in leading custom web solutions from planning through launch, while contributing hands-on code. Deep knowledge of modern programming languages, frameworks, and best practices.
            </p>
            <div class="hero-stats fade-in">
              <div class="stat scale-in">
                <span class="stat-number gradient-text">4+</span>
                <span class="stat-label">Years Experience</span>
              </div>
              <div class="stat scale-in">
                <span class="stat-number gradient-text">20+</span>
                <span class="stat-label">Projects Completed</span>
              </div>
              <div class="stat scale-in">
                <span class="stat-number gradient-text">100%</span>
                <span class="stat-label">Client Satisfaction</span>
              </div>
            </div>
            <div class="hero-buttons fade-in-up">
              <a href="#contact" class="btn btn-primary hover-glow">
                <i class="fas fa-paper-plane"></i>
                Get In Touch
              </a>
              <a href="/ZOHAIB_KHAN_Resume-PM.pdf" class="btn btn-white hover-glow" download>
                <i class="fas fa-download"></i>
                Download Resume
              </a>
            </div>
          </div>
          <div class="hero-image">
            <div class="profile-card glass-effect hover-lift">
              <div class="profile-image">
                <div class="profile-avatar">
                  <i class="fas fa-user-tie"></i>
                </div>
                <div class="profile-ring"></div>
              </div>
              <div class="profile-info">
                <h3>Zohaib Khan</h3>
                <p>Senior Web Developer</p>
                <div class="profile-badges">
                  <span class="badge"><i class="fas fa-layer-group"></i> Full Stack</span>
                  <span class="badge"><i class="fab fa-laravel"></i> Laravel Expert</span>
                  <span class="badge"><i class="fas fa-users-gear"></i> Team Lead</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">About Me</h2>
        <p class="section-subtitle fade-in-up">Professional Summary & Background</p>
        
        <div class="about-content">
          <div class="about-grid">
            <div class="about-text fade-in-left">
              <h3>Professional Summary</h3>
              <p>
                Tech-savvy Web Development professional with strong expertise in Back-end development and Technical Project Management. 
                Specialized in leading custom web solutions from planning through launch, while contributing hands-on code. 
                Deep knowledge of modern programming languages, frameworks, and best practices.
              </p>
              <p>
                Innovative in translating business and marketing requirements into secure, scalable web applications. 
                Solid foundation in IoT architecture for designing connected systems that integrate physical devices with digital platforms.
              </p>
              
              <div class="about-highlights">
                <div class="highlight-item scale-in hover-lift">
                  <div class="highlight-icon">
                    <span class="icon">Code</span>
                  </div>
                  <div class="highlight-content">
                    <h4>Full Stack Development</h4>
                    <p>Expertise in PHP, Laravel, Vue.js, and modern web technologies for comprehensive web solutions</p>
                  </div>
                </div>
                <div class="highlight-item scale-in hover-lift">
                  <div class="highlight-icon">
                    <span class="icon">Lead</span>
                  </div>
                  <div class="highlight-content">
                    <h4>Technical Leadership</h4>
                    <p>Leading development teams and managing projects from conception to deployment</p>
                  </div>
                </div>
                <div class="highlight-item scale-in hover-lift">
                  <div class="highlight-icon">
                    <span class="icon">IoT</span>
                  </div>
                  <div class="highlight-content">
                    <h4>IoT Architecture</h4>
                    <p>Designing connected systems that integrate physical devices with digital platforms</p>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="about-skills fade-in-right">
              <h3>Core Competencies</h3>
              <div class="skill-bars">
                <div v-for="skill in skills" :key="skill.category" class="skill-item hover-lift">
                  <div class="skill-header">
                    <span class="skill-name">{{ skill.category }}</span>
                    <span class="skill-level gradient-text">{{ skill.level }}%</span>
                  </div>
                  <div class="progress-bar">
                    <div class="progress-fill" :data-level="skill.level" :data-width="skill.level + '%'"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="section bg-secondary">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">Skills & Expertise</h2>
        <p class="section-subtitle fade-in-up">Technical and Professional Competencies</p>
        
        <div class="skills-grid">
          <div v-for="skill in skills" :key="skill.category" class="skill-category scale-in hover-lift">
            <div class="skill-header">
              <h3>{{ skill.category }}</h3>
              <div class="skill-percentage gradient-text">{{ skill.level }}%</div>
            </div>
            <div class="skill-tags">
              <span v-for="item in skill.items" :key="item" class="skill-tag hover-glow">{{ item }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="section">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">Professional Experience</h2>
        <p class="section-subtitle fade-in-up">Career Journey & Achievements</p>
        
        <div class="timeline">
          <div v-for="(job, index) in experience" :key="index" class="timeline-item" :class="index % 2 === 0 ? 'fade-in-left' : 'fade-in-right'">
            <div class="timeline-dot"></div>
            <div class="timeline-content hover-lift">
              <div class="timeline-header">
                <div>
                  <h3>{{ job.title }}</h3>
                  <p class="timeline-company">{{ job.company }}</p>
                  <p class="timeline-location">{{ job.location }}</p>
                </div>
                <div class="timeline-period">{{ job.period }}</div>
              </div>
              <div class="timeline-responsibilities" v-if="job.responsibilities">
                <h4>Key Responsibilities:</h4>
                <div class="responsibility-tags">
                  <span v-for="resp in job.responsibilities" :key="resp" class="responsibility-tag">{{ resp }}</span>
                </div>
              </div>
              <ul class="timeline-achievements">
                <li v-for="achievement in job.achievements" :key="achievement">{{ achievement }}</li>
              </ul>
              <div class="timeline-technologies">
                <span v-for="tech in job.technologies" :key="tech" class="tech-tag">{{ tech }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section id="education" class="section bg-secondary">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">Education</h2>
        <p class="section-subtitle fade-in-up">Academic Background & Qualifications</p>
        
        <div class="education-grid">
          <div v-for="(edu, index) in education" :key="index" class="education-card scale-in hover-lift">
            <div class="education-header">
              <div class="education-icon">
                <span class="icon">Edu</span>
              </div>
              <div class="education-info">
                <h3>{{ edu.degree }}</h3>
                <p class="education-institution">{{ edu.institution }}</p>
                <p class="education-location">{{ edu.location }}</p>
              </div>
              <div class="education-period">{{ edu.period }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">Featured Projects</h2>
        <p class="section-subtitle fade-in-up">Recent Work & Portfolio</p>
        
        <div class="project-filters fade-in">
          <button 
            v-for="filter in ['all', 'package', 'crm', 'travel', 'cleaning', 'iot', 'web']" 
            :key="filter"
            :class="['filter-btn', { active: activeFilter == filter }]"
            @click="setActiveFilter(filter)"
          >
            {{ filter.charAt(0).toUpperCase() + filter.slice(1) }}
          </button>
        </div>
        
        <div class="projects-grid">
          <div v-for="project in filteredProjects" :key="project.id" class="project-card scale-in hover-lift">
            <div class="project-image">
              <div class="project-placeholder">{{ project.image }}</div>
              <div class="project-overlay">
                <div class="project-details">
                  <h4>{{ project.role }}</h4>
                  <p>Budget: {{ project.budget }}</p>
                  <a v-if="project.link" :href="project.link" target="_blank" class="btn btn-white">View Project</a>
                  <span v-else class="btn btn-white">Private Project</span>
                </div>
              </div>
            </div>
            <div class="project-content">
              <div class="project-header">
                <h3>{{ project.title }}</h3>
                <span class="project-category">{{ project.category }}</span>
              </div>
              <p>{{ project.description }}</p>
              <div class="project-meta">
                <div class="meta-item">
                  <span class="meta-label">Duration:</span>
                  <span class="meta-value">{{ project.duration }}</span>
                </div>
                <div class="meta-item">
                  <span class="meta-label">Team:</span>
                  <span class="meta-value">{{ project.teamSize }}</span>
                </div>
                <div class="meta-item">
                  <span class="meta-label">Impact:</span>
                  <span class="meta-value">{{ project.impact }}</span>
                </div>
              </div>
              <div class="project-tags">
                <span v-for="tag in project.tags" :key="tag" class="tag">{{ tag }}</span>
              </div>
              <div class="project-technologies">
                <span v-for="tech in project.technologies" :key="tech" class="tech-badge">{{ tech }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Hobbies Section -->
    <section id="hobbies" class="section bg-secondary">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">Hobbies & Interests</h2>
        <p class="section-subtitle fade-in-up">Beyond Coding</p>
        
        <div class="hobbies-grid">
          <div v-for="(hobby, index) in hobbies" :key="index" class="hobby-card scale-in hover-lift">
            <div class="hobby-icon">
              <i :class="hobby.icon"></i>
            </div>
            <h3>{{ hobby.name }}</h3>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section">
      <SectionAmbientBg />
      <div class="container">
        <h2 class="section-title fade-in">Get In Touch</h2>
        <p class="section-subtitle fade-in-up">Let's discuss your next project</p>
        
        <div class="contact-content">
          <div class="contact-info fade-in-left">
            <div class="contact-card hover-lift">
              <h3>Contact Information</h3>
              <div class="contact-items">
                <div class="contact-item">
                  <div class="contact-icon">
                    <i class="fas fa-envelope"></i>
                  </div>
                  <div>
                    <h4>Email</h4>
                    <p>zohaibkhan4822@gmail.com</p>
                  </div>
                </div>
                
                <div class="contact-item">
                  <div class="contact-icon">
                    <i class="fas fa-phone"></i>
                  </div>
                  <div>
                    <h4>Phone</h4>
                    <p>+923062228262</p>
                  </div>
                </div>
                
                <div class="contact-item">
                  <div class="contact-icon">
                    <i class="fas fa-location-dot"></i>
                  </div>
                  <div>
                    <h4>Location</h4>
                    <p>Karachi, Sindh 75230</p>
                  </div>
                </div>
                
                <div class="contact-item">
                  <div class="contact-icon">
                    <i class="fab fa-github"></i>
                  </div>
                  <div>
                    <h4>GitHub</h4>
                    <p>github.com/Zohaib482</p>
                  </div>
                </div>
              </div>
              
              <div class="contact-availability">
                <h4>Availability</h4>
                <p>I'm currently available for freelance projects, full-time opportunities, and teaching positions. Feel free to reach out to discuss how I can help your organization achieve its goals.</p>
                <div class="availability-status">
                  <span class="status-dot available"></span>
                  <span>Available for work</span>
                </div>
              </div>
            </div>
          </div>
          
          <div class="contact-form fade-in-right">
            <div class="form-card hover-lift">
              <h3>Send Message</h3>
              <form @submit.prevent="submitForm">
                <div class="form-row">
                  <div class="form-group">
                    <input type="text" v-model="form.name" placeholder="Your Name" required>
                  </div>
                  <div class="form-group">
                    <input type="email" v-model="form.email" placeholder="Your Email" required>
                  </div>
                </div>
                <div class="form-group">
                  <input type="text" v-model="form.subject" placeholder="Subject" required>
                </div>
                <div class="form-group">
                  <textarea v-model="form.message" placeholder="Your Message" rows="6" required></textarea>
                </div>
                <button type="submit" class="btn btn-primary hover-glow">Send Message</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <p>&copy; 2024 Zohaib Khan. All rights reserved.</p>
          <div class="footer-links">
            <a href="#home">Home</a>
            <a href="#about">About</a>
            <a href="#projects">Projects</a>
            <a href="#contact">Contact</a>
            <a href="https://github.com/Zohaib482" target="_blank"><i class="fab fa-github"></i></a>
            <a href="#" target="_blank"><i class="fab fa-linkedin"></i></a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.section > .container {
  position: relative;
  z-index: 1;
}

.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding: 120px 0 80px;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
}

.hero-gradient {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  opacity: 0.95;
}

.hero-name-gradient {
  background: linear-gradient(135deg, #ffffff 0%, #ffd700 50%, #ffffff 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  filter: drop-shadow(0 0 10px rgba(255, 215, 0, 0.3));
}

/* Custom Cursor - Global Visibility */
.custom-cursor-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 10000;
  mix-blend-mode: difference;
}

.cursor-inner {
  position: fixed;
  width: 10px;
  height: 10px;
  background: #ffffff;
  border-radius: 50%;
  pointer-events: none;
  z-index: 10001;
  transform: translate(-50%, -50%);
  will-change: transform;
}

.cursor-outer {
  position: fixed;
  width: 45px;
  height: 45px;
  border: 3px solid #ffffff;
  border-radius: 50%;
  pointer-events: none;
  z-index: 10000;
  transform: translate(-50%, -50%);
  transition: width 0.3s, height 0.3s;
  will-change: transform;
}

/* Mouse Glow Effect */
.mouse-glow {
  position: fixed;
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, rgba(99, 102, 241, 0.15) 0%, transparent 70%);
  pointer-events: none;
  z-index: 1;
  transform: translate(-50%, -50%);
}

.hero-particles {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: radial-gradient(circle at 20% 80%, rgba(255, 255, 255, 0.1) 0%, transparent 50%),
                    radial-gradient(circle at 80% 20%, rgba(255, 255, 255, 0.1) 0%, transparent 50%),
                    radial-gradient(circle at 40% 40%, rgba(255, 255, 255, 0.05) 0%, transparent 50%);
  animation: float 20s ease-in-out infinite;
}

.floating-shapes {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(5px);
}

.shape-1 {
  width: 100px;
  height: 100px;
  top: 20%;
  left: 10%;
  animation: float 8s ease-in-out infinite;
}

.shape-2 {
  width: 60px;
  height: 60px;
  top: 60%;
  right: 15%;
  animation: float 12s ease-in-out infinite reverse;
}

.shape-3 {
  width: 80px;
  height: 80px;
  bottom: 30%;
  left: 70%;
  animation: float 10s ease-in-out infinite;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  color: white;
  position: relative;
  z-index: 1;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  padding: 12px 20px;
  border-radius: 25px;
  font-size: 0.875rem;
  font-weight: 600;
  margin-bottom: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.3);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.status-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #10b981;
  animation: pulse 2s infinite;
}

.hero-title {
  font-family: 'Playfair Display', serif;
  font-size: 4.5rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  line-height: 1.1;
}

.hero-subtitle {
  font-size: 1.75rem;
  font-weight: 300;
  margin-bottom: 2rem;
  color: rgba(255, 255, 255, 0.9);
}

.hero-description {
  font-size: 1.125rem;
  margin-bottom: 3rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.8);
  max-width: 500px;
}

.hero-stats {
  display: flex;
  gap: 2rem;
  margin-bottom: 3rem;
}

.stat {
  text-align: center;
  padding: 1.5rem;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  min-width: 120px;
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: white;
}

.stat-label {
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.8);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
}

.hero-image {
  display: flex;
  justify-content: center;
  align-items: center;
}

.profile-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border-radius: 25px;
  padding: 2.5rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  text-align: center;
  position: relative;
}

.profile-ring {
  position: absolute;
  top: -10px;
  left: -10px;
  right: -10px;
  bottom: -10px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 25px;
  animation: rotate 10s linear infinite;
}

.profile-image {
  width: 220px;
  height: 220px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 2rem;
  font-size: 3.5rem;
  font-weight: bold;
  border: 4px solid rgba(255, 255, 255, 0.3);
  position: relative;
  z-index: 2;
}

.profile-info h3 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: white;
}

.profile-info p {
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 1.5rem;
}

.profile-badges {
  display: flex;
  gap: 0.5rem;
  justify-content: center;
  flex-wrap: wrap;
}

.profile-badges .badge {
  background: rgba(255, 255, 255, 0.2);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.3);
  font-size: 0.75rem;
  padding: 6px 12px;
}

.bg-secondary {
  background-color: var(--bg-secondary);
}

.about-content {
  max-width: 1200px;
  margin: 0 auto;
}

.about-grid {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 4rem;
  align-items: start;
}

.about-text h3 {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 2rem;
  color: var(--text-primary);
}

.about-text p {
  font-size: 1.125rem;
  line-height: 1.8;
  margin-bottom: 2rem;
  color: var(--text-secondary);
}

.about-highlights {
  margin-top: 3rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.highlight-item {
  display: flex;
  align-items: start;
  gap: 1.5rem;
  padding: 2rem;
  background: var(--bg-secondary);
  border-radius: 20px;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.highlight-item:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.highlight-icon {
  width: 60px;
  height: 60px;
  background: var(--bg-gradient);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 0.875rem;
  flex-shrink: 0;
  box-shadow: var(--shadow-md);
}

.highlight-content h4 {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: var(--text-primary);
}

.highlight-content p {
  font-size: 0.875rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

.about-skills h3 {
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 2.5rem;
  color: var(--text-primary);
}

.skill-bars {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.skill-item {
  background: white;
  padding: 2rem;
  border-radius: 20px;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.skill-name {
  font-weight: 600;
  color: var(--text-primary);
  font-size: 1.125rem;
}

.skill-level {
  font-weight: 700;
  font-size: 1.25rem;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2.5rem;
}

.skill-category {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.skill-category:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-xl);
}

.skill-category .skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

body {
  font-family: 'Inter', sans-serif;
  background-color: var(--bg-primary);
  color: var(--text-primary);
  line-height: 1.6;
  overflow-x: hidden;
  font-weight: 400;
  cursor: none; /* Hide default cursor */
}

.skill-category h3 {
  font-size: 1.375rem;
  font-weight: 600;
  color: var(--text-primary);
}

.skill-percentage {
  font-size: 1.25rem;
  font-weight: 700;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.skill-tag {
  background: var(--bg-secondary);
  color: var(--text-secondary);
  padding: 0.75rem 1.25rem;
  border-radius: 25px;
  font-size: 0.875rem;
  font-weight: 500;
  transition: all 0.3s ease;
  border: 1px solid var(--border-color);
}

.skill-tag:hover {
  background: var(--accent-color);
  color: white;
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.timeline {
  max-width: 1000px;
  margin: 0 auto;
  position: relative;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 3px;
  background: var(--border-color);
  transform: translateX(-50%);
}

.timeline-item {
  margin-bottom: 5rem;
  position: relative;
}

.timeline-item:nth-child(odd) .timeline-content {
  margin-right: 50%;
  padding-right: 3rem;
  text-align: right;
}

.timeline-item:nth-child(even) .timeline-content {
  margin-left: 50%;
  padding-left: 3rem;
}

.timeline-dot {
  position: absolute;
  left: 50%;
  top: 20px;
  width: 24px;
  height: 24px;
  background: var(--accent-color);
  border-radius: 50%;
  transform: translateX(-50%);
  border: 4px solid white;
  box-shadow: var(--shadow-lg);
}

.timeline-content {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: var(--shadow-md);
  position: relative;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.timeline-content::before {
  content: '';
  position: absolute;
  top: 20px;
  width: 0;
  height: 0;
  border-style: solid;
}

.timeline-item:nth-child(odd) .timeline-content::before {
  right: -20px;
  border-width: 10px 0 10px 20px;
  border-color: transparent transparent transparent white;
}

.timeline-item:nth-child(even) .timeline-content::before {
  left: -20px;
  border-width: 10px 20px 10px 0;
  border-color: transparent white transparent transparent;
}

.timeline-header {
  display: flex;
  justify-content: space-between;
  align-items: start;
  margin-bottom: 1.5rem;
}

.timeline-content h3 {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-primary);
}

.timeline-company {
  color: var(--accent-color);
  font-weight: 500;
  font-size: 1.125rem;
  margin-bottom: 0.5rem;
}

.timeline-location {
  color: var(--text-secondary);
  font-size: 0.875rem;
}

.timeline-period {
  background: var(--bg-secondary);
  padding: 0.75rem 1.25rem;
  border-radius: 25px;
  font-size: 0.875rem;
  font-weight: 600;
  color: var(--text-secondary);
  border: 1px solid var(--border-color);
}

.timeline-responsibilities {
  margin-bottom: 1.5rem;
}

.timeline-responsibilities h4 {
  font-size: 1rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 1rem;
}

.responsibility-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.responsibility-tag {
  background: var(--bg-secondary);
  color: var(--text-secondary);
  padding: 0.5rem 1rem;
  border-radius: 15px;
  font-size: 0.75rem;
  font-weight: 500;
  border: 1px solid var(--border-color);
}

.timeline-achievements {
  list-style: none;
  padding: 0;
  margin-bottom: 1.5rem;
}

.timeline-achievements li {
  position: relative;
  padding-left: 1.5rem;
  margin-bottom: 1rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

.timeline-achievements li::before {
  content: '>';
  position: absolute;
  left: 0;
  color: var(--accent-color);
  font-weight: bold;
}

.timeline-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background: var(--bg-secondary);
  color: var(--text-secondary);
  padding: 0.5rem 1rem;
  border-radius: 15px;
  font-size: 0.75rem;
  font-weight: 500;
  border: 1px solid var(--border-color);
}

.project-filters {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 4rem;
  flex-wrap: wrap;
}

.filter-btn {
  background: white;
  border: 2px solid var(--border-color);
  padding: 1rem 2rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.filter-btn:hover,
.filter-btn.active {
  background: var(--accent-color);
  color: white;
  border-color: var(--accent-color);
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
  gap: 2.5rem;
}

.project-card {
  background: white;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: var(--shadow-md);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid var(--border-color);
}

.project-card:hover {
  transform: translateY(-12px);
  box-shadow: var(--shadow-2xl);
}

.project-image {
  height: 220px;
  background: var(--bg-gradient);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.project-placeholder {
  font-size: 3.5rem;
  color: white;
  font-weight: bold;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-details {
  text-align: center;
  color: white;
  padding: 2rem;
}

.project-details h4 {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.project-details p {
  margin-bottom: 2rem;
  font-size: 1.125rem;
}

.project-content {
  padding: 2.5rem;
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: start;
  margin-bottom: 1.5rem;
}

.project-content h3 {
  font-size: 1.375rem;
  font-weight: 600;
  color: var(--text-primary);
}

.project-category {
  background: var(--bg-secondary);
  color: var(--text-secondary);
  padding: 0.5rem 1rem;
  border-radius: 15px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
}

.project-content p {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 2rem;
}

.project-meta {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin-bottom: 2rem;
}

.meta-item {
  text-align: center;
  padding: 1rem;
  background: var(--bg-secondary);
  border-radius: 12px;
}

.meta-label {
  display: block;
  font-size: 0.75rem;
  color: var(--text-light);
  margin-bottom: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.meta-value {
  font-size: 0.875rem;
  font-weight: 600;
  color: var(--text-primary);
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tag {
  background: var(--bg-secondary);
  color: var(--text-secondary);
  padding: 0.5rem 1rem;
  border-radius: 15px;
  font-size: 0.75rem;
  font-weight: 500;
}

.project-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-badge {
  background: var(--accent-color);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 15px;
  font-size: 0.75rem;
  font-weight: 500;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  max-width: 1200px;
  margin: 0 auto;
}

.contact-card,
.form-card {
  background: white;
  padding: 3rem;
  border-radius: 20px;
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border-color);
}

.contact-card h3,
.form-card h3 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 2.5rem;
  color: var(--text-primary);
}

.contact-items {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-bottom: 2.5rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.contact-icon {
  width: 60px;
  height: 60px;
  background: var(--bg-gradient);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 0.875rem;
  flex-shrink: 0;
  box-shadow: var(--shadow-md);
}

.contact-item h4 {
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: var(--text-primary);
}

.contact-item p {
  color: var(--text-secondary);
}

.contact-availability h4 {
  font-size: 1.125rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: var(--text-primary);
}

.contact-availability p {
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.availability-status {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.status-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--accent-color);
  animation: pulse 2s infinite;
}

.status-dot.available {
  background: #10b981;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.form-group {
  margin-bottom: 2rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1.25rem;
  border: 2px solid var(--border-color);
  border-radius: 12px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: var(--bg-secondary);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--accent-color);
  background: white;
  box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1);
}

.footer {
  background-color: var(--bg-dark);
  color: white;
  padding: 3rem 0;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-links {
  display: flex;
  gap: 2rem;
}

.footer-links a {
  color: white;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-links a:hover {
  color: var(--accent-light);
}

.education-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
  max-width: 1000px;
  margin: 0 auto;
}

.education-card {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.education-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-xl);
}

.education-header {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.education-icon {
  width: 60px;
  height: 60px;
  background: var(--bg-gradient);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 0.875rem;
  flex-shrink: 0;
  box-shadow: var(--shadow-md);
}

.education-info {
  flex: 1;
}

.education-info h3 {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  color: var(--text-primary);
}

.education-institution {
  color: var(--accent-color);
  font-weight: 500;
  margin-bottom: 0.25rem;
}

.education-location {
  color: var(--text-secondary);
  font-size: 0.875rem;
}

.education-period {
  background: var(--bg-secondary);
  padding: 0.75rem 1.25rem;
  border-radius: 25px;
  font-size: 0.875rem;
  font-weight: 600;
  color: var(--text-secondary);
  border: 1px solid var(--border-color);
}

.hobbies-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  max-width: 800px;
  margin: 0 auto;
}

.hobby-card {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border-color);
  text-align: center;
  transition: all 0.3s ease;
}

.hobby-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-xl);
}

.hobby-icon {
  width: 80px;
  height: 80px;
  background: var(--bg-gradient);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 1rem;
  margin: 0 auto 1.5rem;
  box-shadow: var(--shadow-lg);
}

.hobby-card h3 {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-primary);
}

/* Custom Cursor */
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 9999;
}

.cursor-inner {
  position: fixed;
  width: 8px;
  height: 8px;
  background: white;
  border-radius: 50%;
  pointer-events: none;
  z-index: 10000;
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
}

.cursor-outer {
  position: fixed;
  width: 35px;
  height: 35px;
  border: 2px solid white;
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
}


/* Enhanced Particle Effects */
.particle {
  position: absolute;
  width: 4px;
  height: 4px;
  background: var(--accent-color);
  border-radius: 50%;
  opacity: 0.6;
  animation: floatParticle 5s infinite ease-in-out;
}

/* Enhanced Background Animations */
.hero-gradient {
  /* Gradient shift animation removed */
}

/* Enhanced Hover Effects */
.hover-lift {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.hover-lift:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

/* Mouse Glow Effect */
.mouse-glow {
  position: fixed;
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, var(--accent-color) 0%, transparent 70%);
  pointer-events: none;
  z-index: 9997;
  transform: translate(-50%, -50%);
  opacity: 0.1;
  animation: glowPulse 3s infinite;
}

/* Enhanced Button Animations */
.btn {
  position: relative;
  overflow: hidden;
  transition: all 0.3s ease;
}

.btn::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: width 0.6s, height 0.6s;
}

.btn:hover::before {
  width: 300px;
  height: 300px;
}

/* Ripple Effect */
.ripple {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.6);
  transform: scale(0);
  animation: rippleEffect 0.6s ease-out;
  pointer-events: none;
}

/* Enhanced Card Animations */
.project-card, .skill-category, .education-card, .hobby-card, .contact-card, .form-card {
  position: relative;
  overflow: hidden;
}

.project-card::before, .skill-category::before, .education-card::before, .hobby-card::before, .contact-card::before, .form-card::before {
  content: '';
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(45deg, var(--accent-color), var(--accent-light), var(--primary-color));
  border-radius: inherit;
  opacity: 0;
  z-index: -1;
  transition: opacity 0.3s ease;
}

.project-card:hover::before, .skill-category:hover::before, .education-card:hover::before, .hobby-card:hover::before, .contact-card:hover::before, .form-card:hover::before {
  opacity: 0.3;
}

/* Floating Animation Enhancements */
@keyframes floatParticle {
  0%, 100% { 
    transform: translateY(0) translateX(0) scale(1);
    opacity: 0.6;
  }
  25% { 
    transform: translateY(-20px) translateX(10px) scale(1.2);
    opacity: 0.8;
  }
  50% { 
    transform: translateY(-10px) translateX(-10px) scale(0.8);
    opacity: 0.4;
  }
  75% { 
    transform: translateY(-30px) translateX(5px) scale(1.1);
    opacity: 0.7;
  }
}

@keyframes gradientShift {
  0%, 100% { 
    background: linear-gradient(135deg, var(--accent-color), var(--accent-light));
  }
  25% { 
    background: linear-gradient(225deg, var(--accent-light), var(--primary-color));
  }
  50% { 
    background: linear-gradient(315deg, var(--primary-color), var(--accent-color));
  }
  75% { 
    background: linear-gradient(45deg, var(--accent-color), var(--accent-light));
  }
}

@keyframes cursorPulse {
  0%, 100% { 
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
  50% { 
    transform: translate(-50%, -50%) scale(1.5);
    opacity: 0.5;
  }
}

@keyframes trailFade {
  0% { 
    opacity: 0.3;
    transform: translate(-50%, -50%) scale(1);
  }
  100% { 
    opacity: 0;
    transform: translate(-50%, -50%) scale(2);
  }
}

@keyframes glowPulse {
  0%, 100% { 
    opacity: 0.1;
    transform: translate(-50%, -50%) scale(1);
  }
  50% { 
    opacity: 0.2;
    transform: translate(-50%, -50%) scale(1.2);
  }
}

@keyframes rippleEffect {
  to {
    transform: scale(4);
    opacity: 0;
  }
}

/* Hide default cursor on interactive elements */
.hover-lift, .btn, .filter-btn, .project-card, .skill-category, .education-card, .hobby-card, .contact-card, .form-card {
  cursor: none !important;
}

/* Enhanced Scroll Animations */
.fade-in.visible, .fade-in-left.visible, .fade-in-right.visible, .fade-in-up.visible, .scale-in.visible, .rotate-in.visible {
  animation-duration: 0.8s;
  animation-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}

/* Interactive Background Elements */
.interactive-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: -1;
  overflow: hidden;
}

.interactive-bg::before {
  content: '';
  position: absolute;
  width: 150%;
  height: 150%;
  top: -25%;
  left: -25%;
  background: radial-gradient(circle at var(--mouse-x, 50%) var(--mouse-y, 50%), rgba(74, 144, 226, 0.1) 0%, transparent 50%);
  transform: translate(-50%, -50%);
}

@media (max-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }
  
  .hero-title {
    font-size: 3rem;
  }
  
  .hero-subtitle {
    font-size: 1.5rem;
  }
  
  .hero-description {
    max-width: 100%;
  }
  
  .hero-stats {
    justify-content: center;
    flex-wrap: wrap;
  }
  
  .hero-buttons {
    justify-content: center;
    flex-wrap: wrap;
  }
  
  .about-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .skills-grid {
    grid-template-columns: 1fr;
  }
  
  .timeline::before {
    left: 30px;
  }
  
  .timeline-item:nth-child(odd) .timeline-content,
  .timeline-item:nth-child(even) .timeline-content {
    margin-left: 60px;
    margin-right: 0;
    padding-left: 0;
    padding-right: 0;
    text-align: left;
  }
  
  .timeline-item:nth-child(odd) .timeline-content::before,
  .timeline-item:nth-child(even) .timeline-content::before {
    left: -20px;
    right: auto;
    border-width: 10px 20px 10px 0;
    border-color: transparent white transparent transparent;
  }
  
  .timeline-dot {
    left: 30px;
  }
  
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .project-meta {
    grid-template-columns: 1fr;
  }
  
  .contact-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .form-row {
    grid-template-columns: 1fr;
  }
  
  .footer-content {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }
  
  .footer-links {
    justify-content: center;
  }
}
</style>
