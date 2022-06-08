<script>
  import {
    useLoaderData,
    Form,
    useActionData,
    useNavigate,
    useNavigation,
  } from "remix-router-vue";
import { computed } from "vue";

  export async function loader() {
    // Load your data here and return whatever you need access to in the UI
    const resp = await fetch(
      "https://randomapi.com/api/6de6abfedb24f889e0b5f675edc50deb"
    );
    const { results } = await resp.json();
    return { results };
  }

  export async function action({ request }) {
    return {};
  }
</script>

<script setup>
  import {
    IonPage,
    IonContent,
    IonButton,
    IonBackButton,
    IonButtons,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonItem,
    IonLabel,
    IonInput,
    IonSelect,
    IonSelectOption,
    IonList,
  } from "@ionic/vue";
  // Use the useLoaderData composition API method to access the data returned
  // from your loader
  const data = useLoaderData();
  const actionData = useActionData();
  const navigate = useNavigate();
    const navigation = useNavigation();
  const isLoading = computed(() => navigation.value.state !== "idle");
  console.log(isLoading && "IS LOADING...");

  console.log(data?.value?.results);
</script>

<template>
  <IonPage>
    <IonHeader>
      <IonToolbar>
        <IonButtons slot="start"
          ><IonButton @click="navigate(-1)">BACK</IonButton></IonButtons
        >
        <IonTitle>IonicVue w/Remix-Router</IonTitle>
      </IonToolbar>
    </IonHeader>
    <IonContent class="ion-padding">
      <IonList>
        <IonItem v-for="item in data?.results[0]" :key="item?.email">
          <IonLabel>{{ `${item.first} ${item.last}` }}</IonLabel>
          <!-- <IonInput type="text" placeholder="name" name="Name"></IonInput> -->
        </IonItem>
      </IonList>
    </IonContent>
  </IonPage>
</template>
