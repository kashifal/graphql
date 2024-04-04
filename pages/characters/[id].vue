<script setup lang="ts">
type Character = {
  character: {
    name: string;
    image: string;
    status: string;
    id: string;
    species: string;
    location: {
      name: string;
    };
  };
};

const route = useRoute();

const query = gql`
  query getCharacter($id: ID!) {
    character(id: $id) {
      name
      image
      status
      id
      species
      location {
        name
      }
    }
  }
`;
const { data, error } = await useAsyncQuery<Character>(query, {
  id: route.params.id,
});
</script>

<template>
  <div class="bg-gray-800 py-20 min-h-screen">
    <div class="max-w-3xl mx-auto">
      <NuxtLink to="/" class="ml-3 text-lg underline py-6 text-white"
        >Back</NuxtLink
      >
      <CharacterCard
        :id="data.character.id"
        :name="data.character.name"
        :image="data.character.image"
        :status="data.character.status"
        :species="data.character.species"
        :location="data.character.location.name"
      />
    </div>
  </div>
</template>
