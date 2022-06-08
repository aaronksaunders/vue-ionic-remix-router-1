<script setup>
  import { useRouteError, useLocation, Link } from "remix-router-vue";
  const location = useLocation();
  const error = useRouteError();
  console.log(error);
</script>

<template>
  <div>
    <h2>ERROR !!</h2>
    <p>Error:{{ JSON.stringify(error.message) }}</p>
    <p>Location:{{ JSON.stringify(location) }}</p>
    <Link to="/"> Go Home </Link>
  </div>
</template>
