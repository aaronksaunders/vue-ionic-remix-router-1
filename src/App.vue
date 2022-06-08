<script setup>
  import { DataBrowserRouter } from "remix-router-vue";

  import Layout from "./Layout.vue";
  import Index, {
    loader as indexLoader,
    action as indexAction,
  } from "./Index.vue";
  import List, { loader as listLoader, action as listAction } from "./List.vue";
  import ErrorVue from "./Error.vue";
import { h } from "vue";

  // Define your routes in a nested array, providing loaders
  // and actions where appropriate
  const routes = [
    {
      path: "/",
      element: Layout,
      errorElement: ErrorVue,
      children: [
        {
          index: true,
          loader: indexLoader,
          action: indexAction,
          element: Index,
          errorElement: ErrorVue,
        },
        {
          path: "list",
          loader: listLoader,
          action: listAction,
          element: List,
          errorElement: ErrorVue,
        },
      ],
    },
  ];

  // Provide a fallbackElement to be displayed during the initial data load
  const fallbackElement = () => h("p", "Loading...");
</script>

<template>
  <DataBrowserRouter :routes="routes"
   :fallbackElement="fallbackElement" />
</template>
