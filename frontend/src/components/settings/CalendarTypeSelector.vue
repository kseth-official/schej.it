<template>
  <v-card class="tw-p-4 sm:tw-p-6">
    <v-expand-transition>
      <div v-show="state === states.PICK_CALENDAR">
        <v-card-title class="tw-px-0 tw-pt-0"
          >Choose a calendar provider</v-card-title
        >
        <v-card-text class="tw-p-0">
          <div class="tw-flex tw-flex-col tw-gap-2">
            <v-btn block @click="$emit('addGoogleCalendar')">
              <div class="tw-flex tw-w-full tw-items-center tw-gap-2">
                <v-img
                  class="tw-flex-initial"
                  width="20"
                  height="20"
                  src="@/assets/google_logo.svg"
                />
                <v-spacer />
                Google Calendar
                <v-spacer />
              </div>
            </v-btn>
            <v-btn block @click="state = states.APPLE_CREDENTIALS">
              <div class="tw-flex tw-w-full tw-items-center tw-gap-2">
                <v-img
                  class="tw-flex-initial"
                  width="20"
                  height="20"
                  src="@/assets/apple_logo.svg"
                />
                <v-spacer />
                Apple Calendar
                <v-spacer />
              </div>
            </v-btn>
            <v-btn block @click="$emit('addOutlookCalendar')">
              <div class="tw-flex tw-w-full tw-items-center tw-gap-2">
                <v-img
                  class="tw-flex-initial"
                  width="20"
                  height="20"
                  src="@/assets/outlook_logo.svg"
                />
                <v-spacer />
                Outlook Calendar
                <v-spacer />
              </div>
            </v-btn>
          </div>
        </v-card-text>
      </div>
    </v-expand-transition>
    <v-expand-transition>
      <AppleCredentials
        v-if="state === states.APPLE_CREDENTIALS"
        @back="state = states.PICK_CALENDAR"
        @addedAppleCalendar="$emit('addedAppleCalendar')"
      />
    </v-expand-transition>
  </v-card>
</template>

<script>
import AppleCredentials from "@/components/calendar_permission_dialogs/AppleCredentials.vue"

export default {
  name: "CalendarTypeSelector",

  components: {
    AppleCredentials,
  },

  data() {
    return {
      states: {
        PICK_CALENDAR: "pick-calendar",
        APPLE_CREDENTIALS: "apple-credentials",
      },
      state: "pick-calendar",
    }
  },
}
</script>
