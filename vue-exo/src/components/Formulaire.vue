<template>
  <div>
    <h1>Connexion</h1>
    <form style="display: flex; flex-direction: column; gap: 20px;">
      <div style="display: flex; flex-direction: column;">
        <label for="email">Email</label>
        <BasicInput v-model="email" type="email" name="email" id="email" required />
      </div>

      <div style="display: flex; flex-direction: column;">
        <label for="password">Mot de passe</label>
        <BasicInput v-model="password" type="password" name="password" id="password" required />
      </div>
      
      <input @click.prevent="login" type="submit" value="Connexion">
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import BasicInput from './BasicInput.vue';

const email = ref('');
const password = ref('');

const login = async () => {

  if (!email || !password) {
    alert('Tous les champs doivent être remplis.');
    return;
  }

  const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;

  if (!emailPattern.test(email.value)) {
    alert('Veuillez entrer une adresse email valide.');
    return;
  }

  if (password.value.length < 8) {
    alert('Le mot de passe doit contenir au moins 8 caractères.');
    return;
  }

  try {
    const response = await fetch('http://localhost:3000/login', {
      method: 'POST',
      headers: {
        'Content-type': 'application/json',
      },
      body: JSON.stringify({
        email: email.value,
        password: password.value
      }),
    })

    const data = await response.json()

    alert((data.msg));

  } catch (e) {
    console.log(e)
  }
}
</script>