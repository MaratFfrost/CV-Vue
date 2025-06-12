<template>
  <section class="services-section">
    <div class="section-header">
      <h2 class="section-title">What I Do</h2>
      <div class="section-divider"></div>
    </div>

    <div class="services-grid">
      <div class="service-card" v-for="(service, index) in services" :key="index" @mouseenter="hoverCard(index)"
        @mouseleave="resetCard(index)" :style="{ transform: service.hover ? 'translateY(-10px)' : 'translateY(0)' }">
        <div class="service-icon" :style="{ color: service.color }">
          <i :class="service.icon"></i>
        </div>
        <h3 class="service-title">{{ service.title }}</h3>
        <p class="service-description">{{ service.description }}</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "ServicesSection",
  data() {
    return {
      services: [
        {
          title: "Web Development",
          description: "Building responsive and performant web applications using modern technologies such as Vue.js and Python.",
          icon: "fas fa-code",
          color: "#42b883",
          hover: false
        },
        {
          title: "Backend Services",
          description: "Developing robust server-side applications and APIs using Python for your business needs. ",
          icon: "fas fa-server",
          color: "#3178c6",
          hover: false
        },
        {
          title: "UI/UX Design",
          description: "Creating intuitive user interfaces with attention to user experience details.",
          icon: "fas fa-paint-brush",
          color: "#fb61da",
          hover: false
        },
      ]
    }
  },
  methods: {
    hoverCard(index) {
      this.services[index].hover = true;
    },
    resetCard(index) {
      this.services[index].hover = false;
    }
  }
}
</script>

<style scoped>
.services-section {
  margin-top: 100px;
  color: white;
  padding-left: 15%;
  padding-right: 15%;
  margin-bottom: 100px;
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-title {
  font-size: 2.2rem;
  font-weight: 700;
  margin-bottom: 15px;
  position: relative;
  display: inline-block;
}

.section-divider {
  width: 80px;
  height: 3px;
  background-color: #4dabf7;
  margin: 0 auto;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;

  margin: 0 auto;
}

.service-card {
  background-color: #1e1e1e;
  border-radius: 10px;
  padding: 30px;
  transition: all 0.3s ease;
  border: 1px solid #333;
}

.service-card:hover {
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.service-icon {
  font-size: 2.5rem;
  margin-bottom: 20px;
  transition: transform 0.3s ease;
}

.service-card:hover .service-icon {
  transform: scale(1.1);
}

.service-title {
  font-size: 1.5rem;
  margin-bottom: 15px;
  font-weight: 600;
  color: #f8f9fa;
}

.service-description {
  color: #adb5bd;
  line-height: 1.6;
  font-size: 1rem;
}

@media (max-width: 768px) {
  .services-section {
    padding: 60px 15px;
  }

  .section-title {
    font-size: 1.8rem;
  }

  .services-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

@media (max-width: 480px) {
  .services-section {
    padding: 50px 10px;
  }

  .section-title {
    font-size: 1.6rem;
  }

  .service-card {
    padding: 25px;
  }
}
</style>
