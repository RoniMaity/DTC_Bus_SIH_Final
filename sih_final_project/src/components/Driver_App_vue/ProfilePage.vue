<template>
  <div class="profile-form">
    <div v-if="!isEditing">
      <div class="profile-info">
        <div class="profile-photo">
          <img :src="profilePhotoUrl" alt="Profile Photo" />
        </div>

        <div class="profile-details">
          <h2 class="name">{{ formData.name || 'Your Name' }}</h2>
          <p><strong>Phone:</strong> {{ formData.phone || 'Not provided' }}</p>
          <p><strong>Date of Birth:</strong> {{ formData.dob || 'Not provided' }}</p>
          <p><strong>Email:</strong> {{ formData.email || 'Not provided' }}</p>
          <p><strong>Gender:</strong> {{ formData.gender || 'Not provided' }}</p>
          <p><strong>Address:</strong> {{ formData.address || 'Not provided' }}</p>
          <p><strong>Bio:</strong> {{ formData.bio || 'Not provided' }}</p>

          <button @click="editProfile" class="edit-btn">Edit Profile</button>
        </div>
      </div>
    </div>

    <div v-else>
      <form @submit.prevent="submitForm" class="form-container">
        <h2 class="form-title">Edit Profile</h2>

        <div class="form-group">
          <label for="profilePhoto" class="profile-photo-circle-label">
            <div class="profile-photo-circle" @click="triggerFileInput">
              <img :src="profilePhotoUrl" alt="Profile Photo" />
            </div>
            <input
              ref="profilePhotoInput"
              type="file"
              id="profilePhoto"
              accept="image/*"
              @change="handleFileUpload"
              style="display: none"
            />
          </label>
        </div>

        <div class="form-group">
          <label for="name">Name</label>
          <input
            type="text"
            v-model="formData.name"
            id="name"
            required
            placeholder="Enter your full name"
          />
        </div>

        <div class="form-group">
          <label for="phone">Phone Number</label>
          <input
            type="tel"
            v-model="formData.phone"
            id="phone"
            required
            placeholder="Enter your phone number"
          />
        </div>

        <div class="form-group">
          <label for="dob">Date of Birth</label>
          <input type="date" v-model="formData.dob" id="dob" required />
        </div>

        <div class="form-group">
          <label for="email">Email</label>
          <input
            type="email"
            v-model="formData.email"
            id="email"
            required
            placeholder="Enter your email"
          />
        </div>

        <div class="form-group">
          <label for="gender">Gender</label>
          <select v-model="formData.gender" id="gender" required>
            <option value="" disabled>Select gender</option>
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            <option value="Other">Other</option>
          </select>
        </div>

        <div class="form-group">
          <label for="address">Address</label>
          <textarea
            v-model="formData.address"
            id="address"
            rows="3"
            placeholder="Enter your address"
          ></textarea>
        </div>

        <div class="form-group">
          <label for="bio">Bio</label>
          <textarea
            v-model="formData.bio"
            id="bio"
            rows="4"
            placeholder="Tell us about yourself"
          ></textarea>
        </div>

        <div class="form-group">
          <button type="submit" class="submit-btn">Save Changes</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      profilePhotoUrl: 'https://via.placeholder.com/150',
      formData: {
        name: '',
        phone: '',
        dob: '',
        email: '',
        gender: '',
        address: '',
        bio: '',
      },
    };
  },
  created() {
    const savedData = JSON.parse(localStorage.getItem('profileData'));
    if (savedData) {
      this.formData = savedData;
      this.profilePhotoUrl = savedData.profilePhotoUrl || this.profilePhotoUrl;
      this.isEditing = false;
    }
  },
  methods: {
    editProfile() {
      this.isEditing = true;
    },
    triggerFileInput() {
      this.$refs.profilePhotoInput.click();
    },
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file && file.type.startsWith('image/')) {
        const reader = new FileReader();
        reader.onload = () => {
          this.profilePhotoUrl = reader.result;
        };
        reader.readAsDataURL(file);
      }
    },
    submitForm() {
      localStorage.setItem('profileData', JSON.stringify({ ...this.formData, profilePhotoUrl: this.profilePhotoUrl }));
      alert('Profile updated successfully!');
      this.isEditing = false;
      location.reload();
    },
  },
};
</script>

<style scoped>
body {
  background: linear-gradient(45deg, #6a11cb, #2575fc);
  font-family: 'Roboto', sans-serif;
  margin: 0;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 200px;
}

.profile-form {
  max-width: 700px;
  width: 100%;
  background-color: rgba(255, 255, 255, 0.9);
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 100px 390px;
}

.profile-form:hover {
  transform: scale(1.02);
}

.profile-photo {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  display: inline-block;
  margin-left: auto;
  margin-right: auto;
}

.profile-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.profile-photo-circle-label {
  display: block;
  text-align: center;
}

.profile-photo-circle {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  display: inline-block;
  margin-left: auto;
  margin-right: auto;
}

.profile-photo-circle img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.profile-photo-circle img:hover {
  transform: scale(1.1);
}

.form-title {
  text-align: center;
  font-size: 26px;
  font-weight: bold;
  color: #333;
  margin-bottom: 30px;
}

.profile-info {
  text-align: center;
}

.profile-details {
  font-size: 16px;
  color: #444;
}

.profile-details p {
  margin-bottom: 15px;
}

.name {
  font-size: 32px;
  font-weight: bold;
  color: #333;
  margin-bottom: 20px;
}

.edit-btn,
.submit-btn {
  padding: 12px 30px;
  background: linear-gradient(45deg, #2575fc, #6a11cb);
  color: white;
  font-size: 16px;
  font-weight: 600;
  border-radius: 50px;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
}

.edit-btn:hover,
.submit-btn:hover {
  background: linear-gradient(45deg, #6a11cb, #2575fc);
  transform: scale(1.05);
}

.form-group {
  margin-bottom: 20px;
}

label {
  font-size: 14px;
  color: #555;
  margin-bottom: 8px;
  font-weight: bold;
}

input,
select,
textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 10px;
  font-size: 14px;
  background-color: #f7f7f7;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

input:focus,
select:focus,
textarea:focus {
  border-color: #2575fc;
  box-shadow: 0 0 8px rgba(37, 117, 252, 0.4);
  outline: none;
}

input[type="file"] {
  display: none;
}

.submit-btn {
  font-size: 18px;
  font-weight: bold;
  width: 100%;
}

@media (max-width: 768px) {
  .profile-form {
    padding: 20px;
    margin: 0;
  }

  .form-title {
    font-size: 22px;
  }

  .form-group input,
  .form-group select,
  .form-group textarea {
    padding: 10px;
  }

  .edit-btn,
  .submit-btn {
    font-size: 14px;
    padding: 10px 25px;
  }
}
</style>
