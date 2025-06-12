<template>
  <header id="header" class="header">
    <div class="header-container">
      <div class="profile-section">
        <div class="photo-placeholder">
          <img v-if="photoUrl" :src="photoUrl" class="photo">
          <div v-else class="photo-initials">ММ</div>
        </div>
        <div class="name-title">
          <h1 class="name">{{ name }}</h1>
          <h2 class="title">{{ position }}</h2>
        </div>
      </div>

      <button class="menu-button" @click="toggleMenu" :class="{ 'active': isMenuOpen }">
        <span class="menu-icon"></span>
      </button>

      <nav class="nav" :class="{ 'active': isMenuOpen }">
        <ul class="nav-list">
          <li class="nav-item">
            <button @click="scrollToSection('portfolio')">Contacts</button>
          </li>
          <li class="nav-item">
            <button @click="scrollToSection('resume')">Work experience</button>
          </li>
          <li class="nav-item">
            <button @click="scrollToSection('resume')">Education</button>
          </li>
          <li class="nav-item">
            <button @click="scrollToSection('resume')">Skills</button>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  name: "ResumeHeader",
  props: {
    name: String,
    photoUrl: String,
    position: String
  },
  data() {
    return {
      isMenuOpen: false,
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    scrollToSection(sectionId) {
      const element = document.getElementById(sectionId)
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' })
        this.isMenuOpen = false
      }
    }
  }
}
</script>

<style scoped>
.header {
  background-color: #000;
  color: rgb(255, 255, 255);
  padding: 1rem;
  width: 100%;
  top: 0;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  border-bottom: 1px solid #333;
}

.header-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.profile-section {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.photo-placeholder {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
  border: 2px solid #fff;
}

.photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.photo-initials {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #333;
  color: white;
  font-weight: bold;
  font-size: 1.5rem;
}

.name {
  font-size: 1.5rem;
  margin: 0;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.title {
  font-size: 0.9rem;
  margin: 0.3rem 0 0 0;
  font-weight: 400;
  color: #979696;
}

.nav {
  display: flex;
}

.nav-list {
  display: flex;
  list-style: none;
  margin: 0;
  margin-right: 25px;
  gap: 2rem;
}

.nav-item button {
  background: none;
  border: none;
  font-family: inherit;
  font-size: 1rem;
  color: rgb(255, 255, 255);
  cursor: pointer;
  padding: 0.8rem 0;
  position: relative;
  transition: color 0.3s;
}

.nav-item button::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background-color: rgb(255, 255, 255);
  transition: width 0.3s;
}

.nav-item button:hover::after {
  width: 100%;
}

.menu-button {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  z-index: 1001;
}

.menu-icon {
  display: block;
  width: 25px;
  height: 2px;
  background-color: rgb(255, 255, 255);
  position: relative;
  transition: background-color 0.3s;
}

.menu-icon::before,
.menu-icon::after {
  content: '';
  position: absolute;
  width: 25px;
  height: 2px;
  background-color: rgb(255, 255, 255);
  left: 0;
  transition: transform 0.3s;
}

.menu-icon::before {
  top: -8px;
}

.menu-icon::after {
  top: 8px;
}

@media (max-width: 768px) {
  .header {
    padding: 0.8rem;
    position: fixed;
  }

  .profile-section {
    gap: 0.8rem;
  }

  .photo-placeholder {
    width: 80px;
    height: 80px;
  }

  .name {
    font-size: 1.3rem;
  }

  .title {
    font-size: 0.8rem;
  }

  .nav {
    position: fixed;
    top: 0;
    left: -100%;
    width: 80%;
    max-width: 300px;
    height: 100vh;
    background-color: #000;
    flex-direction: column;
    padding: 6rem 2rem;
    box-shadow: 5px 0 15px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s ease-in-out;
    z-index: 1000;
  }

  .nav.active {
    transform: translateX(100%);
  }

  .nav-list {
    flex-direction: column;
    gap: 2rem;
    width: 100%;
    margin-right: 0;
  }

  .nav-item {
    width: 100%;
  }

  .nav-item button {
    width: 100%;
    padding: 1rem;
    color: white;
    font-size: 1.2rem;
  }

  .nav-item button::after {
    background-color: #4dabf7;
  }

  .menu-button {
    display: block;
    margin-right: 5%;
    position: relative;
    z-index: 1001;
  }

  .menu-button.active .menu-icon {
    background-color: transparent;
  }

  .menu-button.active .menu-icon::before {
    transform: rotate(45deg);
    top: 0;
    background-color: white;
  }

  .menu-button.active .menu-icon::after {
    transform: rotate(-45deg);
    top: 0;
    background-color: white;
  }
}

@media (max-width: 480px) {
  .photo-placeholder {
    width: 70px;
    height: 70px;
  }

  .photo-initials {
    font-size: 1.2rem;
  }

  .name {
    font-size: 1.1rem;
  }
}
</style>
