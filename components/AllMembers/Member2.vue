<template>
  <v-content>
    <v-container>
      <v-layout>
        <v-flex>
          <v-row>
            <v-col
              cols="12"
              xs="12"
              sm="6"
              md="4"
              lg="3"
              xl="2"
              v-for="(member, index) in membersArray2"
              :key="index"
            >
              <v-hover>
                <template v-slot:default="{ hover }">
                  <v-card
                    dark
                    class="member-card"
                    :to="member.to"
                    width="230px"
                    height="400px"
                    :ripple="true"
                    style="background-color:black;"
                  >
                    <v-img class="member-img" :src="member.src"></v-img>
                    <v-card-title class="member-title" v-text="member.name">
                    </v-card-title>
                    <v-card-subtitle v-text="member.subname"> </v-card-subtitle>
                    <v-card-text v-text="member.number"> </v-card-text>
                    <v-fade-transition>
                      <v-overlay
                        v-if="hover"
                        absolute
                        color="#555555"
                      ></v-overlay>
                    </v-fade-transition>
                  </v-card>
                </template>
              </v-hover>
            </v-col>
          </v-row>
        </v-flex>
      </v-layout>
    </v-container>
  </v-content>
</template>

<script>
import firebase from "firebase";
export default {
  data() {
    return {
      membersArray2: []
    };
  },
  created() {
    const that = this;
    const members = firebase
      .firestore()
      .collection("members2")
      .orderBy("subname", "asc");
    members.get().then(snapshot => {
      snapshot.forEach(doc => {
        const members = doc.data();
        that.membersArray2 = [
          ...that.membersArray2,
          {
            name: members.name,
            subname: members.subname,
            src: members.src,
            from: members.from,
            old: members.old,
            birth: members.birth,
            number: members.number,
            to: members.to
          }
        ];
      });
    });
  }
};
</script>

<style></style>
