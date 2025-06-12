<template>
  <section id="resume" class="resume-section">
    <div class="section-header">
      <h2 class="section-title">My Resume</h2>
      <div class="section-divider"></div>
    </div>

    <div class="tabs-container">
      <div class="tabs-header">
        <button v-for="(tab, index) in tabs" :key="index" @click="activeTab = index"
          :class="{ 'active': activeTab === index }" class="tab-button">
          {{ tab.title }}
        </button>
      </div>

      <div class="tabs-content">
        <transition name="fade" mode="out-in">
          <div v-if="activeTab === 0" class="tab-panel">
            <h3 class="panel-title">Professional Bio</h3>
            <p class="bio-text">
              {{ bioText }}
            </p>
            <div class="bio-highlights">
              <div v-for="(item, index) in bioHighlights" :key="index" class="highlight-item">
                <i class="fas fa-check highlight-icon"></i>
                <span>{{ item }}</span>
              </div>
            </div>
          </div>

          <div v-else-if="activeTab === 1" class="tab-panel">
            <h3 class="panel-title">Technical Skills</h3>
            <div class="skills-grid">
              <div v-for="(skill, index) in skills" :key="index" class="skill-block"
                :style="{ borderColor: skill.color }">
                <div class="skill-block-header">
                  <i :class="skill.icon" class="skill-icon" :style="{ color: skill.color }"></i>
                  <span class="skill-name">{{ skill.name }}</span>
                </div>
                <div class="skill-tags">
                  <span v-for="(tag, tagIndex) in skill.tags" :key="tagIndex" class="skill-tag">
                    {{ tag }}
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div v-else-if="activeTab === 2" class="tab-panel">
            <h3 class="panel-title">Professional Experience</h3>
            <div class="timeline">
              <div v-for="(item, index) in experience" :key="index" class="timeline-item">
                <div class="timeline-period">{{ item.period }}</div>
                <div class="timeline-content">
                  <h4>{{ item.position }}</h4>
                  <a :href=item.link class="institution">{{ item.company }}</a>
                  <ul class="experience-list">
                    <li v-for="(responsibility, i) in item.responsibilities" :key="i">
                      <i class="fas fa-caret-right"></i> {{ responsibility }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>

          <div v-else class="tab-panel">
            <h3 class="panel-title">Education</h3>
            <div class="timeline">
              <div v-for="(item, index) in education" :key="index" class="timeline-item">
                <div class="timeline-period">{{ item.period }}</div>
                <div class="timeline-content">
                  <h4>{{ item.degree }}</h4>
                  <p class="institution">{{ item.institution }}</p>
                  <p class="description">{{ item.description }}</p>
                </div>
              </div>
            </div>
          </div>
        </transition>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "ResumeTabs",
  props: ['bioText'],
  data() {
    return {
      activeTab: 0,
      tabs: [
        { title: "Bio" },
        { title: "Skills" },
        { title: "Experience" },
        { title: "Education" }
      ],
      experience: [
        {
          period: "2023 - Present",
          position: "Full Stack Developer",
          company: "MVlab",
          link: "http://www.mvlabby.iron.hostflyby.net/",
          responsibilities: [
            "Developed responsive web applications using Vue.js and Django",
            "Implemented RESTful APIs with Django REST Framework",
            "Optimized application performance through code refactoring",
            "Collaborated with clients to translate requirements into technical solutions"
          ]
        },
      ],
      bioHighlights: [
        "Specialized in Vue.js, Django, FastAPI",
        "Cloud architecture expertise",
        "Agile/Scrum methodology",
        "CI/CD pipelines implementation"
      ],
      skills: [
        {
          name: "Frontend",
          icon: "fas fa-code",
          color: "#42b883",
          tags: ["Vue.js", "Vuex", "TypeScript", "HTML/CSS", "Tailwind"]
        },
        {
          name: "Backend",
          icon: "fas fa-server",
          color: "#3178c6",
          tags: ["Python", "Django", "FastAPI", "GraphQL", "REST API"]
        },
        {
          name: "DevOps",
          icon: "fas fa-cloud",
          color: "#2496ed",
          tags: ["Docker", "Docker Compose", "CI/CD", "Nginx", "Cubernetes"]
        },
        {
          name: "Database",
          icon: "fas fa-database",
          color: "#00758f",
          tags: ["PostgreSQL", "MongoDB", "Redis", "SQL", "SqlAlchemy", "DjangoORM"]
        },
        {
          name: "Tools",
          icon: "fas fa-tools",
          color: "#fb61da",
          tags: ["Git", "VS Code", "Figma", "Postman"]
        },
      ],
      education: [
        {
          period: "2023-present",
          degree: "Master's in Computer Science",
          institution: "Belorussian State University",
          description: "Specialized in Software Engineering and Web Technologies"
        },
      ]
    }
  }
}
</script>

<style scoped>
.resume-section {
  padding-top: 50px;
  padding-right: 15%;
  padding-left: 15%;
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
  margin: 0 auto;
}

.tabs-container {
  margin: 0 auto;
  background-color: #1e1e1e;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
}

/* Стили табов */
.tabs-header {
  display: flex;
  border-bottom: 1px solid #333;
}

.tab-button {
  flex: 1;
  padding: 20px;
  background: none;
  border: none;
  color: #adb5bd;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
}

.tab-button:hover {
  color: white;
}

.tab-button.active {
  color: white;
}

.tab-button.active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 3px;
  background-color: #4dabf7;
}

.tabs-content {
  padding: 40px;
}

.panel-title {
  font-size: 1.8rem;
  margin-bottom: 30px;
  color: #f8f9fa;
}

/* Стили для вкладки Bio */
.bio-text {
  color: #adb5bd;
  line-height: 1.8;
  margin-bottom: 30px;
  font-size: 1.1rem;
}

.bio-highlights {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.highlight-item {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #e9ecef;
}

.highlight-icon {
  color: #4dabf7;
}

/* Стили для вкладки Skills */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 25px;
}

.skill-block {
  background-color: #252525;
  border-radius: 8px;
  padding: 20px;
  border-left: 4px solid;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.skill-block:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.skill-block-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 15px;
}

.skill-icon {
  font-size: 1.8rem;
}

.skill-name {
  font-size: 1.3rem;
  font-weight: 600;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-tag {
  background-color: #333;
  color: #e9ecef;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.85rem;
}

/* Стили для вкладки Education */
.timeline {
  position: relative;
  padding-left: 30px;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 7px;
  top: 0;
  height: 100%;
  width: 2px;
  background-color: #4dabf7;
}

.timeline-item {
  position: relative;
  padding-bottom: 30px;
}

.timeline-item:last-child {
  padding-bottom: 0;
}

.timeline-item::before {
  content: '';
  position: absolute;
  left: -30px;
  top: 5px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background-color: #4dabf7;
  border: 3px solid #121212;
}

.timeline-period {
  color: #4dabf7;
  font-weight: 600;
  margin-bottom: 10px;
}

.timeline-content {
  background-color: #252525;
  padding: 20px;
  border-radius: 8px;
}

.timeline-content h4 {
  margin: 0 0 5px 0;
  font-size: 1.2rem;
}

.institution {
  color: #adb5bd;
  margin-bottom: 10px;
  font-style: italic;
}

.description {
  color: #e9ecef;
  line-height: 1.6;
}

/* Анимации */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Адаптивность */
@media (max-width: 768px) {
  .tabs-header {
    flex-direction: column;
  }

  .tab-button {
    padding: 15px;
    text-align: center;
  }

  .tabs-content {
    padding: 30px 20px;
  }

  .panel-title {
    font-size: 1.5rem;
    margin-bottom: 20px;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .resume-section {
    padding: 60px 15px;
  }

  .section-title {
    font-size: 1.8rem;
  }

  .bio-highlights {
    grid-template-columns: 1fr;
  }

  .skill-block-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 5px;
  }
}
</style>
