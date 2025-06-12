<template>
  <section class="portfolio-section">
    <div class="section-header">
      <h2 class="section-title">My Projects</h2>
      <div class="section-divider"></div>
      <p class="section-subtitle">Here are some of my recent works</p>
    </div>

    <div class="portfolio-grid">
      <div v-for="(project, index) in projects" :key="index" class="portfolio-item">
        <div class="portfolio-overlay">
          <div class="portfolio-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <div class="project-tech">
              <span v-for="(tech, i) in project.technologies" :key="i" class="tech-tag">
                {{ tech }}
              </span>
            </div>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-links">
              <a v-if="project.codeLink" :href="project.codeLink" target="_blank" rel="noopener noreferrer"
                class="project-link">
                <i class="fab fa-github"></i> View Code
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "PortfolioSection",
  data() {
    return {
      projects: [
        {
          title: "Tic Tac Toe Game",
          description: "Full-featured online store with payment integration and admin dashboard",
          technologies: ["JavaScript", "HTML", "CSS",],
          codeLink: "https://github.com/MaratFfrost/Tic-Tac-Toe.git"
        },
        {
          title: "FastAPI REST API",
          description: "RESTful API for managing tasks and users with authentication and authorization",
          technologies: ["Python", "FastAPI", "SQLAlchemy", "Celery", "Redis"],
          codeLink: "https://github.com/MaratFfrost/fastapi_internet_shop.git"
        },
        {
          title: "FastAPI Notion API",
          description: "Rest API for managing notions and users",
          technologies: ["FastAPI", "Beanie", "MongoDB"],
          codeLink: 'https://github.com/MaratFfrost/Notion.git'
        },
        {
          title: "More projects are in github",
          description: "",
          technologies: [],
          codeLink: "https://github.com/MaratFfrost"
        },
      ]
    }
  }
}
</script>

<style scoped>
.portfolio-section {
  padding-top: 70px;
  padding-left: 15%;
  padding-right: 15%;
  color: white;
  font-family: 'Montserrat', sans-serif;
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-title {
  font-size: 2.2rem;
  font-weight: 700;
  margin-bottom: 15px;
}

.section-divider {
  width: 80px;
  height: 3px;
  background-color: #4dabf7;
  margin: 10px auto 20px;
}

.section-subtitle {
  color: #adb5bd;
  font-size: 1.1rem;
  max-width: 600px;
  margin: 0 auto;
}

.portfolio-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 30px;
  margin: 0 auto;
}

.portfolio-item {
  background-color: #252525;
  height: 350px;
  background-size: cover;
  background-position: center;
  border-radius: 10px;
  position: relative;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.portfolio-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  opacity: 1;
  transition: opacity 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.portfolio-item:hover .portfolio-overlay {
  opacity: 1;
}

.portfolio-item:hover {
  transform: translateY(-10px);
}

.portfolio-content {
  text-align: center;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.portfolio-item:hover .portfolio-content {
  transform: translateY(0);
}

.project-title {
  font-size: 1.5rem;
  margin-bottom: 15px;
  color: #f8f9fa;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
  margin-bottom: 15px;
}

.tech-tag {
  background-color: #252525;
  color: #e9ecef;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
}

.project-description {
  color: #adb5bd;
  line-height: 1.6;
  margin-bottom: 20px;
}

.project-links {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  padding: 8px 15px;
  background-color: #4dabf7;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-size: 0.9rem;
  transition: background-color 0.3s ease;
}

.project-link:hover {
  background-color: #3a8fd4;
}

.project-link i {
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .portfolio-grid {
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  }

  .portfolio-item {
    height: 300px;
  }

  .section-title {
    font-size: 1.8rem;
  }
}

@media (max-width: 480px) {
  .portfolio-section {
    padding: 60px 15px;
  }

  .portfolio-grid {
    grid-template-columns: 1fr;
  }

  .project-links {
    flex-direction: column;
    align-items: center;
  }

  .project-link {
    width: 100%;
    justify-content: center;
  }
}
</style>
