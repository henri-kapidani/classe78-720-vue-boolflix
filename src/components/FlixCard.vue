<template>
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img
          v-if="imgUrl"
          :src="imgUrl"
          :alt="title"
        >
        <img
          v-else
          src="@/assets/img/default.jpg"
          :alt="title"
        >
      </div>

      <div class="flip-card-back">
        <div>
          Titolo: {{ title }}
        </div>
        <div>
          Titolo originale: {{ originalTitle }}
        </div>

        <lang-flag :iso="language" />
        <div class="language-textual">
          {{ language }}
        </div>

        <div class="score">
          <font-awesome-icon
            v-for="i in score.score"
            :key="i"
            icon="fa-solid fa-star"
            :style="{ color: 'yellow' }"
          />
          <font-awesome-icon
            v-for="i in (score.maxScore - score.score)"
            :key="(i + score.maxScore)"
            icon="fa-regular fa-star"
            :style="{ color: 'yellow' }"
          />
        </div>

        <div class="cast">
          Cast: {{ cast.join(', ') }}
        </div>

        <p>
          <!-- eslint-disable-next-line -->
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem. Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur error pariatur aut veritatis molestiae iusto mollitia ipsum, labore nisi itaque repellat quidem doloremque et voluptate soluta excepturi obcaecati voluptatem.
        </p>
      </div>
    </div>
  </div>

  <!-- <div>
    <ul>
      <li>
        <img
          v-if="imgUrl"
          :src="imgUrl"
          :alt="title"
        >
        <img
          v-else
          src="@/assets/img/default.jpg"
          :alt="title"
        >
      </li>
      <li>{{ title }}</li>
      <li>{{ originalTitle }}</li>
      <li>
        <lang-flag :iso="language" />
        <span class="language-textual">{{ language }}</span>
      </li>
      <font-awesome-icon
        v-for="i in score.score"
        :key="i"
        icon="fa-solid fa-star"
        :style="{ color: 'yellow' }"
      />
      <font-awesome-icon
        v-for="i in (score.maxScore - score.score)"
        :key="(i + score.maxScore)"
        icon="fa-regular fa-star"
        :style="{ color: 'yellow' }"
      />
    </ul>
  </div> -->
</template>

<script>
import LangFlag from 'vue-lang-code-flags';

export default {
  name: 'FlixCard',
  components: {
    LangFlag,
  },
  props: {
    title: String,
    originalTitle: String,
    language: String,
    score: Object,
    imgUrl: String,
    cast: { // TODO: Perche' non lo prende?
      type: Array,
      default() {
        return [];
      },
    },
  },
};
</script>

<style lang="scss" scoped>
  .flip-card {
    // margin: 2rem;
    padding: 1rem;
    // border: 2px solid green;
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }

  .flag-icon-undefined,
  .language-textual {
    display: none;
  }

  .flag-icon-undefined ~ .language-textual {
    display: block;
  }

  /* The flip card container - set the width and height to whatever
  you want. We have added the border property to demonstrate that
  the flip itself goes out of the box on hover (remove perspective
  if you don't want the 3D effect */
.flip-card {
  // background-color: transparent;
  // width: 300px;
  height: 400px;
  // border: 1px solid #f1f1f1;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
}

/* This container is needed to position the front and back side */
.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  // text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  // background-color: #bbb;
  // color: black;
}

/* Style the back side */
.flip-card-back {
  background-color: black;
  color: white;
  transform: rotateY(180deg);
  overflow-y: auto;
}
</style>
