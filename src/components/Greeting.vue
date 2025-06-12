<template>
  <section id="portfolio" class="hero-section">
    <div class="hero-content">
      <div class="text-content">
        <h1 class="name-title">Welcome To My Portfolio</h1>
        <h3 class="profession">I'm a {{ position }}</h3>
        <p class="description">
          {{ description }}
        </p>

        <div class="social-buttons">
          <a v-for="social in socialLinks" :key="social.name" :href="social.url" target="_blank"
            rel="noopener noreferrer" class="social-button" :style="{ backgroundColor: social.color }">
            <i :class="social.icon"></i>
            <span>{{ social.name }}</span>
          </a>
        </div>
      </div>

      <div class="interactive-element" ref="interactiveElement">
        <div class="tech-bubble" v-for="(tech, index) in techs" :key="index" :style="bubbleStyle(tech, index)"
          @mouseenter="hoverTech(index)" @mouseleave="resetTech(index)">
          <span class="tech-name">{{ tech.name }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    position: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    technologies: {
      type: Array,
      required: true,
      validator: value => value.length > 0
    },
    socialLinks: {
      type: Array,
      required: true,
      validator: value => value.length > 0
    }
  },
  data() {
    return {
      techs: [],
      containerSize: { width: 0, height: 0 },
    }
  },
  mounted() {
    this.initTechBubbles();
    window.addEventListener('resize', this.handleResize);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    initTechBubbles() {
      if (this.$refs.interactiveElement) {
        this.containerSize = {
          width: this.$refs.interactiveElement.offsetWidth,
          height: this.$refs.interactiveElement.offsetHeight
        };

        this.techs = this.technologies.map(techName => ({
          name: techName,
          size: Math.floor(Math.random() * 30) + 50,
          color: this.getRandomColor(),
          hover: false,
          x: Math.random() * (this.containerSize.width - 100),
          y: Math.random() * (this.containerSize.height - 100)
        }));
      }
    },
    getRandomColor() {
      const colors = [
        '#42b883', '#61dafb', '#68a063', '#3178c6',
        '#2496ed', '#fb61da', '#a06368', '#c6318c'
      ];
      return colors[Math.floor(Math.random() * colors.length)];
    },
    bubbleStyle(tech, index) {
      return {
        left: `${tech.x}px`,
        top: `${tech.y}px`,
        width: `${tech.size}px`,
        height: `${tech.size}px`,
        backgroundColor: tech.color,
        animationDelay: `${index * 0.2}s`,
        zIndex: tech.hover ? 10 : 1,
        transform: tech.hover ? 'scale(1.1)' : 'scale(1)'
      };
    },
    hoverTech(index) {
      this.techs[index].hover = true;
      this.techs[index].size += 15;
    },
    resetTech(index) {
      this.techs[index].hover = false;
      this.techs[index].size -= 15;
    },
    handleResize() {
      this.initTechBubbles();
    }
  }
}
</script>

<style scoped>
.hero-section {
  margin-top: 25px;
  color: white;
}

.hero-content {
  margin: 0 auto;
  display: flex;
  padding-top: 70px;
  padding-left: 15%;
  padding-right: 15%;
  justify-content: space-between;
}

.text-content {
  flex: 1;
  max-width: 600px;
}

.name-title {
  font-size: 2.5rem;
  margin-bottom: 20px;
  font-weight: 700;
  line-height: 1.2;
}

.profession {
  color: #4dabf7;
  font-size: 1.5rem;
  margin-bottom: 20px;
  font-weight: 600;
}

.description {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #e9ecef;
  margin-bottom: 30px;
}

.interactive-element {
  position: relative;
  width: 300px;
  height: 300px;
  margin-right: 50px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  overflow: hidden;
}

.tech-bubble {
  position: absolute;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  transform-origin: center;
  animation: float 6s ease-in-out infinite;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.tech-name {
  opacity: 0;
  transition: opacity 0.3s ease;
  font-size: 0.8rem;
  text-align: center;
  padding: 5px;
}

.tech-bubble:hover {
  transform: scale(1.1);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

.tech-bubble:hover .tech-name {
  opacity: 1;
}

.social-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 40px;
}

.social-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 10px 20px;
  color: white;
  text-decoration: none;
  border-radius: 30px;
  font-weight: 500;
  transition: all 0.3s ease;
  font-size: 0.9rem;
  min-width: 120px;
}

.social-button i {
  margin-right: 8px;
  font-size: 1.1rem;
}

.social-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

@keyframes float {

  0%,
  100% {
    transform: translateY(0) rotate(0deg);
  }

  50% {
    transform: translateY(-10px) rotate(3deg);
  }
}

@media (max-width: 1250px) {
  .interactive-element {
    display: none;
    width: 100%;
    height: 250px;
    margin-top: 30px;
  }
}

@media (max-width: 768px) {
  .hero-content {
    flex-direction: column;
    text-align: center;
  }

  .interactive-element {
    display: none;
    width: 100%;
    height: 250px;
    margin-top: 30px;
  }

  .name-title {
    font-size: 2rem;
  }

  .profession {
    font-size: 1.3rem;
  }

  .social-buttons {
    justify-content: center;
  }

  .social-button {
    padding: 8px 16px;
    font-size: 0.8rem;
    min-width: 100px;
  }
}

@media (max-width: 480px) {
  .hero-section {
    padding: 60px 15px;
  }

  .name-title {
    font-size: 1.8rem;
  }

  .profession {
    font-size: 1.2rem;
  }

  .description {
    font-size: 1rem;
  }
}
</style>
