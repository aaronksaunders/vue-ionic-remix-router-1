<script>
  import {
    useLoaderData,
    Form,
    useActionData,
    Link,
    useNavigation,
  } from "remix-router-vue";
  import { computed } from "vue";

  export async function loader() {
    // Load your data here and return whatever you need access to in the UI
    debugger;
    return { message: "this is a test" };
  }

  export async function action({ request }) {
    debugger;
    const body = await request.formData();
    return {
      name: body.get("name"),
      email: body.get("email"),
      shirtColor: body.get("shirtColor"),
    };
  }
</script>

<script setup>
  import {
    IonPage,
    IonContent,
    IonButton,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonItem,
    IonLabel,
    IonInput,
    IonSelect,
    IonSelectOption,
    IonLoading,
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardTitle,
  } from "@ionic/vue";
  // Use the useLoaderData composition API method to access the data returned
  // from your loader
  const data = useLoaderData();
  const actionData = useActionData();
  const navigation = useNavigation();
  const isSaving = computed(() => navigation.value.state !== "idle");
</script>

<template>
  <IonPage>
    <IonHeader>
      <IonToolbar>
        <IonTitle>IonicVue w/Remix-Router</IonTitle>
      </IonToolbar>
    </IonHeader>
    <IonContent class="ion-padding">
      <IonLoading :is-open="isSaving" message="Loading..."></IonLoading>
      <p>Check out my data!</p>
      <pre>{{ data }}</pre>
      <p>Check out my action data!</p>
      <pre>{{ actionData }}</pre>
      <IonCard>
        <IonCardHeader>
          <IonCardTitle>Testing Form Submission </IonCardTitle>
        </IonCardHeader>
        <IonCardContent>
          <Form method="post" action="/?index">
            <IonItem>
              <IonLabel position="floating">Name</IonLabel>
              <IonInput type="text" placeholder="name" name="Name"></IonInput>
            </IonItem>
            <IonItem>
              <IonLabel position="floating">Email</IonLabel>
              <IonInput type="text" placeholder="email" name="email"></IonInput>
            </IonItem>
            <IonItem>
              <IonLabel>Select</IonLabel>
              <IonSelect name="shirtColor">
                <IonSelectOption value="brown">Brown</IonSelectOption>
                <IonSelectOption value="blonde">Blonde</IonSelectOption>
                <IonSelectOption value="black">Black</IonSelectOption>
                <IonSelectOption value="red">Red</IonSelectOption>
              </IonSelect>
            </IonItem>
            <div style="margin-top: 8px">
              <IonButton
                type="submit"
                :disabled="isSaving"
                style="margin-right: 8px"
                >SAVE</IonButton
              >
              <Link to="/list">
                <IonButton :disabled="isSaving">GOTO LIST PAGE</IonButton>
              </Link>
            </div>
          </Form>
        </IonCardContent>
      </IonCard>
    </IonContent>
  </IonPage>
</template>
