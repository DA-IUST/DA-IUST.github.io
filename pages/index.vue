<template>
  <v-row justify="center" align="center">
    <v-col lg="1" xl="1" cols="0"/>
    <v-col lg="10" xl="10" cols="12" class="justify-center">

      <div class="yellow lighten-3 elevation-6 pa-2">
        <div class="pa-5">
          <div class="d-flex align-center justify-center">
            <v-img :src="LOGO" max-width="100"/>
          </div>
          <div :class="`text-center ${textSize.courseTitle} pa-2`">{{course.title}}</div>
        </div>


        <div v-if="isMainMenuVisible"
             class="d-flex align-center justify-center">

          <v-btn
            v-for="(item, index) in menu"
            :key="index"
            color="black"
            v-ripple="{ class: `light-blue--text` }"
            :style="page===item.pageName ? 'background-color: #B3E5FC' : ''"
            @click="page=item.pageName"
            tile
            text
            large>
            {{item.text}}
            <v-icon class="ml-2">{{item.icon}}</v-icon>
          </v-btn>

        </div>
      </div>

      <div class="pa-2">
        <about v-show="page===HOME_PAGE" :people="people" :course-description="course.description"/>
        <Schedule v-show="page===SCHEDULE_PAGE" :events="schedule.events"/>
        <Assignments v-show="page===ASSIGNMENT_PAGE" :assignments="assignments"/>
        <Assignments v-show="page===PROJECT_PAGE" :assignments="projects"/>
        <CourseMaterials v-show="page===COURSE_MATERIAL_PAGE" :materials="materials"/>
      </div>

      <div v-if="!isMainMenuVisible" class="bottom-nav">
        <v-bottom-navigation
          color="blue">

          <v-btn v-for="(item, index) in bottomNavigationMenu" :key="index" @click="page=item.pageName">
            <span class="text-caption pt-1">{{item.text}}</span>
            <v-icon>{{item.icon}}</v-icon>
          </v-btn>


        </v-bottom-navigation>
      </div>

    </v-col>
    <v-col lg="1" xl="1" cols="0"/>
  </v-row>
</template>

<script>

  import About from "../components/About";
  import Footer from "../components/Footer";
  import CourseMaterials from "../components/CourseMaterials";
  import Assignments from "../components/Assignments";
  import Schedule from "../components/Schedule";

  const HOME_PAGE = 'home';
  const SCHEDULE_PAGE = 'schedule';
  const ASSIGNMENT_PAGE = 'assignments';
  const PROJECT_PAGE = 'projects';
  const COURSE_MATERIAL_PAGE = 'materials';

  // Site Images
  const LOGO = require('../static/images/iust.png');

  // Profile images
  const MALE_PROFILE = require('../static/images/profile-boy.jpg');
  const FEMALE_PROFILE = require('../static/images/profile-girl.jpg');
  const MARZIEH_MALEKI_MAJD = FEMALE_PROFILE;
  const DANI_BAZI = require('../static/images/danial.jpg');
  const ALI_SEDGHI = require('../static/images/ali.jpg');
  const AMIN_GHASVARI = require('../static/images/amin.png');
  const AMIRH_AHMADI = require('../static/images/amir h.jpg');
  const RAMTIN_EHSANI = require('../static/images/ramtin.jpg');
  const MOBINA_KASHANIAN = require('../static/images/mobina.jpg');
  const REZA_GHAHRAMANI = require('../static/images/reza.jpg');
  const SINA_ZIAEE = require('../static/images/sina.jpg');

  // References covers
  const REF_BOOK_1 = require('../static/images/ref_book1.jpg');
  const REF_BOOK_2 = require('../static/images/ref_book2.jpg');
  const CLRS = require('../static/images/clrs.png');
  const CLRS_FILE = 'https://github.com/TLA-IUST/TLA-IUST.github.io/blob/master/static/references/Michael%20Sipser%20-%20Introduction%20to%20the%20Theory%20of%20Computation%20(2012%2C%20Thomson%20South-Western).pdf';

  // Resources Covers
  export default {
    computed: {
      HOME_PAGE: () => HOME_PAGE,
      SCHEDULE_PAGE: () => SCHEDULE_PAGE,
      ASSIGNMENT_PAGE: () => ASSIGNMENT_PAGE,
      PROJECT_PAGE: () => PROJECT_PAGE,
      COURSE_MATERIAL_PAGE: () => COURSE_MATERIAL_PAGE,
      // Images
      LOGO: () => LOGO,
      isMainMenuVisible() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs':
            return false;
          case 'sm':
            return false;
          case 'md':
            return true;
          case 'lg':
            return true;
          case 'xl':
            return true;
        }
      },
      textSize() {
        switch (this.$vuetify.breakpoint.name) {
          case 'xs':
            return {
              courseTitle: 'text-h4',
              courseDescription: 'text-h8',
            };
          case 'sm':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h6',
            };
          case 'md':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h4',
            };
          case 'lg':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h4',
            };
          case 'xl':
            return {
              courseTitle: 'text-h2',
              courseDescription: 'text-h4',
            };
        }
      }
    },
    data: () => ({
      page: HOME_PAGE,

      // Course Details
      course: {
        title: "Algorithm",
        subtitle: "More Details about course",
        description: "Informally, an algorithm is any well-deﬁned computational procedure that takes some value, or set of values, as input and produces some value, or set of values, as output. An algorithm is thus a sequence of computational steps that transform the input into the output...",
      },

      // Main Menu
      menu: [
        {
          pageName: HOME_PAGE,
          text: "Home",
          icon: 'mdi-home'
        },
        {
          pageName: SCHEDULE_PAGE,
          text: "Schedule",
          icon: 'mdi-calendar'
        },
        {
          pageName: ASSIGNMENT_PAGE,
          text: "Assignments",
          icon: 'mdi-book-open'
        },
        {
          pageName: PROJECT_PAGE,
          text: "Projects",
          icon: 'mdi-rocket'
        },
        {
          pageName: COURSE_MATERIAL_PAGE,
          text: "Resources",
          icon: 'mdi-book'
        },
      ],

      // Bottom Navigation
      bottomNavigationMenu: [
        {
          pageName: SCHEDULE_PAGE,
          text: "Schedule",
          icon: 'mdi-calendar'
        },
        {
          pageName: ASSIGNMENT_PAGE,
          text: "Assignments",
          icon: 'mdi-book-open'
        },
        {
          pageName: PROJECT_PAGE,
          text: "Projects",
          icon: 'mdi-rocket'
        },
        {
          pageName: COURSE_MATERIAL_PAGE,
          text: "References",
          icon: 'mdi-book'
        },
      ],

      // Schedule
      schedule: {
        events: [
          {
            name: 'Introduction',
            start: '2021-02-25 18:00',
            end: '2021-02-25 20:00',
            color: 'red'
          },
        ]
      },

      // Assignments
      assignments: [
        // {
        //   name: "Assignment number 1",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 2",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 3",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 4",
        //   file: ''
        // },
        // {
        //   name: "Assignment number 5",
        //   file: ''
        // }
      ],

      // Projects
      projects: [
        // {
        //   name: "Project number 1",
        //   file: ''
        // },
        // {
        //   name: "Project number 2",
        //   file: ''
        // },
        // {
        //   name: "Project number 3",
        //   file: ''
        // }
      ],

      // Characters
      people: {
        professor: {
          name: "‪Marzieh Malekimajd",
          image: FEMALE_PROFILE
        },
        assistants: [
          {
            name: "Danial Bazmandeh",
            image: DANI_BAZI
          },
          {
            name: "Mobina Kashanian",
            image: MOBINA_KASHANIAN
          },
          {
            name: "M.Amin Ghasvari",
            image: AMIN_GHASVARI
          },
          {
            name: "Amir H. Ahmadi",
            image: AMIRH_AHMADI
          },
          {
            name: "Ramtin Ehsani",
            image: RAMTIN_EHSANI
          },
          {
            name: "Ali Sedaghi",
            image: ALI_SEDGHI
          },
          {
            name: "Sina Ziaee",
            image: SINA_ZIAEE
          },
          {
            name: "Reza Ghahremani",
            image: REZA_GHAHRAMANI
          },
          {
            name: "Mostafa MohammadAliEbrahim",
            image: MALE_PROFILE
          },
        ],
      },

      // References
      materials: {
        main: [
          {
            name: "CLRS",
            description: "This book is Reference 1",
            cover: CLRS,
            file: CLRS_FILE
          },
        ],
        additional: [
          // {
          //   name: "Reference 4",
          //   description: "This book is Reference 4",
          //   cover: REF_BOOK_1,
          // }
        ]
      }
    }),
    components: { Schedule, CourseMaterials, Footer, About, Assignments },
  }
</script>

<style scoped lang="scss">
  .bottom-nav {
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;
    z-index: 2;
  }
</style>
