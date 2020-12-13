<template>
  <div>
    <div class="velkomst">
      <h1>Klar til endnu en dag med gang i den og glade kunder?</h1>
      <h3>Lad os få fjernet alle de gamle bookinger!</h3>
      <p>
        Tryk på knappen for at få slettet alle bookinger der er ældre end i dag:
      </p>
      <button class="updateKnap" v-on:click="updatePosts()">
        Slet gamle bookinger!
      </button>
    </div>

    <div class="grid-container">
      <article v-for="post in contacts" :key="post.id">
        <div>
          <h1>Kunde: {{ post.navn }}</h1>
          <p>
            Dato for indlevering: <strong>{{ post.dato }}</strong>
          </p>
          <p>
            Ønsket tid for indlevering: <strong>{{ post.tid }}</strong>
          </p>
          <p>Telefonnummer: {{ post.telefonnummer }}</p>
          <p>Del af cyklen hvor der er problem: {{ post.del }}</p>
          <p>Problemet: {{ post.problem }}</p>
        </div>

        <button class="doneKnap" type="button" v-on:click="sletPost(post.id)">
          Done!
        </button>
      </article>
    </div>
  </div>
</template>

<script>
import { postRef } from "../firebase-db.js"; import { postRefSlet } from
"../firebase-db.js"; export default { data() { return { contacts: [] }; },
methods: { updatePosts() { let today = new Date(); let dagsDato = "" +
today.getFullYear() + (today.getMonth() + 1) + today.getDate();
console.log(dagsDato); let newContacts = []; for (const contact of
this.contacts) { if (Number(contact.internDato) > Number(dagsDato)) {
newContacts.push(contact); } else { postRefSlet.doc(contact.id).delete(); } }
this.contacts = newContacts; }, sletPost(id) { postRefSlet.doc(id).delete(); }
}, firestore: { contacts: postRef } };
</script>

<style>
.updateKnap {
  background-color: #f2cb03;
  text-align: center;
  align-self: flex-end;
  border: none;
  font-size: 16px;
  font-weight: 700;
  border-radius: 28px;
  height: 40px;
  width: 180px;
  color: black;
  margin: auto;
}

.doneKnap {
  background-color: #f2cb03;
  text-align: center;
  align-self: flex-end;
  border: none;
  font-size: 24px;
  font-weight: 700;
  border-radius: 28px;
  height: 48px;
  width: 120px;
  color: black;
  margin: auto;
}
.grid-container {
  display: grid;
  grid-template-columns: 100%;
  grid-gap: 20px 10px;
}

article {
  background-color: #fff;
  border-radius: 20px;
  color: black;
  max-width: 400px;
  width: 100%;
  height: 400px;
  margin: auto;
  display: flex;
  flex-direction: column;
}

article div {
  padding: 20px;
}

h1 {
  color: #f2cb03;
}

.velkomst {
  text-align: center;
  margin-bottom: 40px;
}

@media screen and (min-width: 750px) {
  .grid-container {
    display: grid;
    grid-template-columns: 50% 50%;
  }
}

@media screen and (min-width: 1300px) {
  .grid-container {
    display: grid;
    grid-template-columns: 33% 33% 33%;
  }
}
</style>