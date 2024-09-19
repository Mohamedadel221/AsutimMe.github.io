<template>
  <div class="table-data mt-5">
    <v-container>
      <v-row cols>
        <v-table v-if="allLocations.length > 0">
          <caption>
            List Of Location
            {{
              allLocations
            }}
          </caption>
          <thead>
            <tr>
              <th scope="cols">Name</th>
              <th scope="cols">Phone</th>
              <th scope="cols">Adress</th>
              <th scope="cols">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(loc, i) in allLocations" :key="i">
              <td>{{ loc.name }}</td>
              <td>{{ loc.phone }}</td>
              <td>{{ loc.adress }}</td>
            </tr>
          </tbody>
        </v-table>
        <div
          v-else
          class="alert alert-warning text-capitalize text-center"
          role="warning"
        >
          No location Added Yet
        </div>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  name: "userLocation",
  props: ["allLocations"],
};
</script>
<style></style>
