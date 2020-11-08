<template>
  <div class="row">
      <!--Card Income-->
      <div class="col-lg-4">
        <v-hover
          v-slot:default="{ hover }"
          close-delay="200"
        >
        <v-card
          class="justify-space-between text-center"
          color="green"
          :elevation="hover ? 16 : 2"
          :class="{ 'on-hover': hover }"
          dark
          max-width="400"
        >
          <v-card-text>
            <v-sheet color="rgba(0, 0, 0, .12)">
              <v-sparkline
                :value="value"
                color="rgba(255, 255, 255, .7)"
                height="100"
                padding="24"
                stroke-linecap="round"
                smooth
              >
                <template v-slot:label="item">
                  ${{ item.value }}
                </template>
              </v-sparkline>
            </v-sheet>
          </v-card-text>

          <v-card-text>
            <div class="display-1 font-weight-thin">
              Total Income
            </div>
          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions class="justify-center">
            <v-btn
              block
              text
            >
              Go to Report
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-hover>
      </div>

      <!--Total Sales-->
      <div class="col-lg-4">
      <v-hover
          v-slot:default="{ hover }"
          close-delay="200"
        >
        <v-card
          class="justify-space-between text-center"
          color="red"
          :elevation="hover ? 16 : 2"
          :class="{ 'on-hover': hover }"
          dark
          max-width="400"
        >
          <v-card-text>
            <v-sheet color="rgba(0, 0, 0, .12)">
              <v-sparkline
                :value="value"
                color="rgba(255, 255, 255, .7)"
                height="100"
                padding="24"
                stroke-linecap="round"
                smooth
              >
                <template v-slot:label="item">
                  ${{ item.value }}
                </template>
              </v-sparkline>
            </v-sheet>
          </v-card-text>

          <v-card-text>
            <div class="display-1 font-weight-thin">
              Total Sales
            </div>
          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions class="justify-center">
            <v-btn
              block
              text
            >
              Go to Report
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-hover>
      </div>

      <!--Total Revenue-->
      <div class="col-lg-4">
      <v-hover
          v-slot:default="{ hover }"
          close-delay="200"
        >
        <v-card
          class="justify-space-between   text-center"
          color="purple"
          :elevation="hover ? 16 : 2"
          :class="{ 'on-hover': hover }"
          dark
          max-width="400"
        >
          <v-card-text>
            <v-sheet color="rgba(0, 0, 0, .12)">
              <v-sparkline
                :value="value"
                color="rgba(255, 255, 255, .7)"
                height="100"
                padding="24"
                stroke-linecap="round"
                smooth
              >
                <template v-slot:label="item">
                  ${{ item.value }}
                </template>
              </v-sparkline>
            </v-sheet>
          </v-card-text>

          <v-card-text>
            <div class="display-1 font-weight-thin">
              Total Revenue
            </div>
          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions class="justify-center">
            <v-btn
              block
              text
            >
              Go to Report
            </v-btn>
          </v-card-actions>
        </v-card> 
      </v-hover>
      </div>
  </div>
</template>

<script>
export default {
  data: () => ({
      value: [
        423,
        446,
        675,
        510,
        590,
        610,
        760,
      ],
    }),
}
</script>>