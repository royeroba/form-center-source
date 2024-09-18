<template>
  <div class="form-container">
    <h1 class="title">Test Dynamic Form</h1>
    <div class="card">
      <form @submit.prevent="validateForm">
        <div class="form-group">
          <label for="name">Name:</label>
          <input
            type="text"
            id="name"
            placeholder="Enter your name"
            v-model="name"
            @blur="touchField('name')"
            class="input-field"
          />
          <div v-if="nameError && nameTouched" class="error">
            {{ nameError }}
          </div>
        </div>

        <div class="form-group">
          <label for="email">Email:</label>
          <input
            type="email"
            id="email"
            placeholder="Enter your email"
            v-model="email"
            @blur="touchField('email')"
            class="input-field"
          />
          <div v-if="emailError && emailTouched" class="error">
            {{ emailError }}
          </div>
        </div>

        <div class="form-group">
          <label for="phone">Phone:</label>
          <div class="phone-container">
            <input
              type="tel"
              id="phone"
              placeholder="Enter your phone number"
              v-model="phone"
              @blur="touchField('phone')"
              class="input-field"
            />
            <button
              type="button"
              class="add-phone-button"
              @click="showOtherPhone = true"
            >
              +
            </button>
          </div>
          <div v-if="phoneError && phoneTouched" class="error">
            {{ phoneError }}
          </div>
        </div>

        <div v-if="showOtherPhone" class="form-group">
          <label for="otherPhone">Other Phone:</label>
          <input
            type="tel"
            id="otherPhone"
            placeholder="Enter another phone number"
            v-model="otherPhone"
            @blur="touchField('otherPhone')"
            class="input-field"
          />
          <div v-if="otherPhoneError && otherPhoneTouched" class="error">
            {{ otherPhoneError }}
          </div>
        </div>

        <button type="submit" class="submit-button">Submit</button>
      </form>
    </div>

    <UserData v-if="isSubmitted" :form-data="formData" />
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";
import UserData from "./UserData.vue";

// reactive variables
const name = ref("");
const email = ref("");
const phone = ref("");
const otherPhone = ref("");
const nameTouched = ref(false);
const emailTouched = ref(false);
const phoneTouched = ref(false);
const otherPhoneTouched = ref(false);
const isSubmitted = ref(false);
const showOtherPhone = ref(false);
const formData = ref({ name: "", email: "", phone: "", otherPhone: "" });

// Validations fields with computed
const nameError = computed(() => {
  return name.value.length < 3 ? "The name must be at least 3 characters" : "";
});

const emailError = computed(() => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return !emailRegex.test(email.value) ? "The email must be valid" : "";
});

const phoneError = computed(() => {
  const phoneRegex = /^\d+$/;
  if (!phoneRegex.test(phone.value)) {
    return "Phone number should contain only digits";
  } else if (phone.value.length < 7) {
    return "Phone number should contain only digits and be at least 7 digits long";
  }
  return "";
});

const otherPhoneError = computed(() => {
  if (!showOtherPhone.value) return "";
  const phoneRegex = /^\d+$/;
  if (!phoneRegex.test(otherPhone.value)) {
    return "Other phone should contain only digits";
  } else if (otherPhone.value.length < 7) {
    return "Other phone should be at least 7 digits long";
  }
  return "";
});

// Function field has been touched
const touchField = (field) => {
  if (field === "name") nameTouched.value = true;
  if (field === "email") emailTouched.value = true;
  if (field === "phone") phoneTouched.value = true;
  if (field === "otherPhone") otherPhoneTouched.value = true;
};

//Watch to detect changes in inputs
watch(name, () => {
  if (nameTouched.value) nameError.value;
});

watch(email, () => {
  if (emailTouched.value) emailError.value;
});

watch(phone, () => {
  if (phoneTouched.value) phoneError.value;
});

watch(otherPhone, () => {
  if (otherPhoneTouched.value) otherPhoneError.value;
});

// Send form
const validateForm = () => {
  nameTouched.value = true;
  emailTouched.value = true;
  phoneTouched.value = true;
  otherPhoneTouched.value = true;

  if (
    !nameError.value &&
    !emailError.value &&
    !phoneError.value &&
    !otherPhoneError.value
  ) {
    isSubmitted.value = true;
    formData.value = {
      name: name.value,
      email: email.value,
      phone: phone.value,
      otherPhone: otherPhone.value,
    };
  }
};
</script>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.title {
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  background-color: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
}

.form-group {
  margin-bottom: 20px;
}

.input-field {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
  margin-top: 5px;
}

.input-field:focus {
  outline: none;
  border-color: #ffa500;
}

.phone-container {
  display: flex;
  gap: 10px;
  align-items: center;
}

.add-phone-button {
  background-color: #ffa500;
  color: white;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.add-phone-button:hover {
  background-color: white;
  color: #ffa500;
  border: 2px solid #ffa500;
}

.error {
  color: red;
  font-size: 12px;
  margin-top: 5px;
}

.submit-button {
  width: 100%;
  padding: 12px 0;
  background-color: #ffa500;
  border: none;
  border-radius: 8px;
  font-size: 18px;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  text-align: center;
}

.submit-button:hover {
  background-color: white;
  color: #ffa500;
  border: 2px solid #ffa500;
}
</style>
