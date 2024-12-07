<template>
  <div class="profile-page">
    <div class="profile-photo">
      <img src="src/pages/Doodle.png" alt="Profile Photo" />
    </div>
    <div class="sidebar">
      <ul>
        <li><a href="#" @click="setActiveSection('home')"><i class="fas fa-home"></i> Home <i class="fas fa-chevron-right"></i></a></li>
        <li><a href="#" @click="setActiveSection('profile')"><i class="fas fa-user"></i> Profile <i class="fas fa-chevron-right"></i></a></li>
        <li><a href="#" @click="setActiveSection('settings')"><i class="fas fa-cogs"></i> Settings <i class="fas fa-chevron-right"></i></a></li>
        <li><a href="#" @click="setActiveSection('timetable')"><i class="fas fa-calendar-alt"></i> Timetable <i class="fas fa-chevron-right"></i></a></li>
        <li><a href="#" @click="setActiveSection('helpCenter')"><i class="fas fa-question-circle"></i> Help Center <i class="fas fa-chevron-right"></i></a></li>
        <li><a href="#" @click="setActiveSection('feedback')"><i class="fas fa-comment-dots"></i> Feedback <i class="fas fa-chevron-right"></i></a></li>
      </ul>
      <button class="logout-btn" @click="logout"><i class="fas fa-sign-out-alt"></i> Log Out</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProfilePage',
  data() {
    return {
      activeSection: {
        title: 'Welcome',
        description: 'Please select a section from the sidebar.',
      },
      sections: {
        home: { title: 'Home', description: 'This is your home section.' },
        profile: { title: 'Profile', description: 'Here is your profile information.' },
        settings: { title: 'Settings', description: 'Manage your account settings here.' },
        timetable: { title: 'Timetable', description: 'View your timetable here.' },
        helpCenter: { title: 'Help Center', description: 'Get assistance and find answers to common questions.' },
        feedback: { title: 'Feedback', description: 'Provide your feedback to help improve our service.' },
      },
    };
  },
  methods: {
    logout() {
      alert("You have been logged out.");
    },
    setActiveSection(section) {
      this.activeSection = this.sections[section];
    }
  },
};
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css');

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f5f5f5;
}

.profile-page {
  display: flex;
  height: 100vh;
  border: 2px solid #ddd;
  border-radius: 10px;
  overflow: hidden;
}

.profile-photo {
  width: 100%;
  height: 270px;
  background-color: #3498db;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom-left-radius: 20%;
  border-bottom-right-radius: 20%;
  border-right: 2px solid #ddd;
}

.profile-photo img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid white;
}

.sidebar {
  background-color: #ffffff;
  color: black;
  width: 250px;
  padding: 20px;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
  border-left: 2px solid #ddd;
  display: flex;
  flex-direction: column;
}

.sidebar ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.sidebar ul li {
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 5px;
  transition: all 0.3s ease;
}

.sidebar ul li a {
  color: #333;
  text-decoration: none;
  font-size: 18px;
  font-weight: 500;
  display: flex;
  align-items: center;
  padding: 10px 20px;
  border-radius: 5px;
  transition: all 0.3s ease;
}

.sidebar ul li a i {
  margin-right: 15px;
  font-size: 22px;
}

.sidebar ul li a .fa-chevron-right {
  margin-left: auto;
  font-size: 18px;
  color: #aaa;
  transition: color 0.3s ease;
}

.sidebar ul li:hover {
  border-color: #16a085;
}

.sidebar ul li a:hover {
  background-color: #16a085;
  color: white;
}

.sidebar ul li a:hover .fa-chevron-right {
  color: white;
}

.logout-btn {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 12px 20px;
  width: 100%;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  margin-top: 20px;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.logout-btn:hover {
  background-color: #c0392b;
}

.logout-btn i {
  margin-right: 10px;
}

.content {
  flex: 1;
  padding: 40px;
  background-color: #ffffff;
  box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.05);
  overflow-y: auto;
  border-left: 2px solid #ddd;
}

/* Title Styles */
.content h2 {
  font-size: 28px;
  font-weight: 600;
  color: #333;
  display: flex;
  justify-content: center;  
  align-items: center;      
  text-align: center;      
  padding: 20px 0;          
}

/* Description Styles */
.content p {
  font-size: 18px;
  color: #666;
  line-height: 1.6;
  text-align: center;       
}

@media (min-width: 768px) {
  .profile-page {
    flex-direction: row;
  }

  .profile-photo {
    width: 250px;
    height: 250px;
    margin-right: 30px;
  }

  .sidebar {
    width: 250px;
  }
}

@media (max-width: 767px) {
  .profile-page {
    flex-direction: column;
  }

  .sidebar {
    width: 100%;
    padding: 15px;
    box-shadow: none;
  }
}
</style>
