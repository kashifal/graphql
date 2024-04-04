<template>
  <div class="bg-gray-800">
    <div class="py-20 min-h-screen max-w-7xl mx-auto">
      <Heading />
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4">
        <CharacterCard
          v-for="{ id, name, image, status, species, location } in data
            .characters.results"
          :key="id"
          :id="id"
          :name="name"
          :image="image"
          :status="status"
          :species="species"
          :location="location.name"
        />
      </div>
    </div>
  </div>
</template>
<script lang="ts" setup>
type CharactersResults = {
  characters: {
    results: {
      id: string;
      name: string;
      image: string;
      status: string;
      species: string;
      location: {
        name: string;
      };
    }[];
  };
};

const query = gql`
  query getCharacters {
    characters {
      results {
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
  }
`;
const { data } = await useAsyncQuery<CharactersResults>(query);
</script>
