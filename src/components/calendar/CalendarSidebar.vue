<template>
  <div class="col-xxl-3 col-lg-4">
    <div class="card h-100 p-0">
      <div class="card-body p-24">
        <button type="button"
          class="btn btn-primary text-sm btn-sm px-12 py-12 w-100 radius-8 d-flex align-items-center gap-2 mb-32"
          data-bs-toggle="modal" data-bs-target="#exampleModal">
          <iconify-icon icon="fa6-regular:square-plus" class="icon text-lg line-height-1"></iconify-icon>
          Add Currency
        </button>

        <div class="mt-32">
          <div v-for="(event, index) in events" :key="index"
            class="event-item d-flex align-items-center justify-content-between gap-4 pb-16 mb-16 border border-start-0 border-end-0 border-top-0">
            <div>
              <div class="d-flex align-items-center gap-10">
                <span :class="['w-12-px', 'h-12-px', event.color, 'rounded-circle', 'fw-medium']"></span>
                <span class="text-secondary-light">{{ event.time }}</span>
              </div>
              <span class="text-primary-light fw-semibold text-md mt-4">{{ event.name }}</span>
            </div>
            <div class="dropdown">
              <button type="button" data-bs-toggle="dropdown" aria-expanded="false">
                <iconify-icon icon="entypo:dots-three-vertical" class="icon text-secondary-light"></iconify-icon>
              </button>
              <ul class="dropdown-menu p-12 border bg-base shadow">
                <li>
                  <button type="button"
                    class="dropdown-item px-16 py-8 rounded text-secondary-light bg-hover-neutral-200 text-hover-neutral-900 d-flex align-items-center gap-10"
                    data-bs-toggle="modal" data-bs-target="#exampleModalView">
                    <iconify-icon icon="hugeicons:view" class="icon text-lg line-height-1"></iconify-icon>
                    View
                  </button>
                </li>
                <li>
                  <button type="button"
                    class="dropdown-item px-16 py-8 rounded text-secondary-light bg-hover-neutral-200 text-hover-neutral-900 d-flex align-items-center gap-10"
                    data-bs-toggle="modal" data-bs-target="#exampleModalEdit">
                    <iconify-icon icon="lucide:edit" class="icon text-lg line-height-1"></iconify-icon>
                    Edit
                  </button>
                </li>
                <li>
                  <button type="button"
                    class="delete-item dropdown-item px-16 py-8 rounded text-secondary-light bg-hover-danger-100 text-hover-danger-600 d-flex align-items-center gap-10"
                    data-bs-toggle="modal" data-bs-target="#exampleModalDelete">
                    <iconify-icon icon="fluent:delete-24-regular" class="icon text-lg line-height-1"></iconify-icon>
                    Delete
                  </button>
                </li>
              </ul>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>

  <!-- Modal Add Event -->
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-lg modal-dialog modal-dialog-centered">
      <div class="modal-content radius-16 bg-base">
        <div class="modal-header py-16 px-24 border border-top-0 border-start-0 border-end-0">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Add New Event</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body p-24">
          <form @submit.prevent>
            <div class="row">
              <div class="col-12 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8">Event Title : </label>
                <input type="text" class="form-control radius-8" placeholder="Enter Event Title " v-model="eventData.title" />
              </div>
              <div class="col-md-6 mb-20">
                <label for="startDate" class="form-label fw-semibold text-primary-light text-sm mb-8">Start Date</label>
                <div class="position-relative">
                  <input class="form-control radius-8 bg-base" ref="startDate" type="text" v-model="eventData.startDate"
                    placeholder="03/12/2024, 10:30 AM" />
                  <span class="position-absolute end-0 top-50 translate-middle-y me-12 line-height-1">
                    <iconify-icon icon="solar:calendar-linear" class="icon text-lg"></iconify-icon>
                  </span>
                </div>
              </div>
              <div class="col-md-6 mb-20">
                <label for="endDate" class="form-label fw-semibold text-primary-light text-sm mb-8">End Date</label>
                <div class="position-relative">
                  <input class="form-control radius-8 bg-base" ref="endDate" type="text" v-model="eventData.endDate"
                    placeholder="03/12/2024, 2:30 PM" />
                  <span class="position-absolute end-0 top-50 translate-middle-y me-12 line-height-1">
                    <iconify-icon icon="solar:calendar-linear" class="icon text-lg"></iconify-icon>
                  </span>
                </div>
              </div>

              <!-- Labels -->
              <div class="col-12 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8">Label</label>
                <div class="d-flex align-items-center flex-wrap gap-28">
                  <div class="form-check checked-success d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="Personal" v-model="eventData.label" value="Personal" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="Personal">
                      <span class="w-8-px h-8-px bg-success-600 rounded-circle"></span>
                      Personal
                    </label>
                  </div>
                  <div class="form-check checked-primary d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="Business" v-model="eventData.label" value="Business" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="Business">
                      <span class="w-8-px h-8-px bg-primary-600 rounded-circle"></span>
                      Business
                    </label>
                  </div>
                  <div class="form-check checked-warning d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="Family" v-model="eventData.label" value="Family" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="Family">
                      <span class="w-8-px h-8-px bg-warning-600 rounded-circle"></span>
                      Family
                    </label>
                  </div>
                  <div class="form-check checked-secondary d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="Important" v-model="eventData.label" value="Important" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="Important">
                      <span class="w-8-px h-8-px bg-lilac-600 rounded-circle"></span>
                      Important
                    </label>
                  </div>
                  <div class="form-check checked-danger d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="Holiday" v-model="eventData.label" value="Holiday" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="Holiday">
                      <span class="w-8-px h-8-px bg-danger-600 rounded-circle"></span>
                      Holiday
                    </label>
                  </div>
                </div>
              </div>

              <div class="col-12 mb-20">
                <label for="desc" class="form-label fw-semibold text-primary-light text-sm mb-8">Description</label>
                <textarea class="form-control" id="desc" rows="4" cols="50" placeholder="Write some text" v-model="eventData.description"></textarea>
              </div>

              <div class="d-flex align-items-center justify-content-center gap-3 mt-24">
                <button type="reset"
                  class="border border-danger-600 bg-hover-danger-200 text-danger-600 text-md px-40 py-11 radius-8">
                  Cancel
                </button>
                <button type="submit" @click="saveEvent" class="btn btn-primary border border-primary-600 text-md px-24 py-12 radius-8">
                  Save
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal View Event -->
  <div class="modal fade" id="exampleModalView" tabindex="-1" aria-labelledby="exampleModalViewLabel"
    aria-hidden="true">
    <div class="modal-dialog modal-lg modal-dialog modal-dialog-centered">
      <div class="modal-content radius-16 bg-base">
        <div class="modal-header py-16 px-24 border border-top-0 border-start-0 border-end-0">
          <h1 class="modal-title fs-5" id="exampleModalViewLabel">View Details</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body p-24">
          <div class="mb-12">
            <span class="text-secondary-light txt-sm fw-medium">Title</span>
            <h6 class="text-primary-light fw-semibold text-md mb-0 mt-4">Design Conference</h6>
          </div>
          <div class="mb-12">
            <span class="text-secondary-light txt-sm fw-medium">Start Date</span>
            <h6 class="text-primary-light fw-semibold text-md mb-0 mt-4">25 Jan 2024, 10:30AM</h6>
          </div>
          <div class="mb-12">
            <span class="text-secondary-light txt-sm fw-medium">End Date</span>
            <h6 class="text-primary-light fw-semibold text-md mb-0 mt-4">25 Jan 2024, 2:30AM</h6>
          </div>
          <div class="mb-12">
            <span class="text-secondary-light txt-sm fw-medium">Description</span>
            <h6 class="text-primary-light fw-semibold text-md mb-0 mt-4">N/A</h6>
          </div>
          <div class="mb-12">
            <span class="text-secondary-light txt-sm fw-medium">Label</span>
            <h6 class="text-primary-light fw-semibold text-md mb-0 mt-4 d-flex align-items-center gap-2">
              <span class="w-8-px h-8-px bg-success-600 rounded-circle"></span>
              Business
            </h6>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal Edit Event -->
  <div class="modal fade" id="exampleModalEdit" tabindex="-1" aria-labelledby="exampleModalEditLabel"
    aria-hidden="true">
    <div class="modal-dialog modal-lg modal-dialog modal-dialog-centered">
      <div class="modal-content radius-16 bg-base">
        <div class="modal-header py-16 px-24 border border-top-0 border-start-0 border-end-0">
          <h1 class="modal-title fs-5" id="exampleModalEditLabel">Edit Event</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body p-24">
          <form @submit.prevent>
            <div class="row">
              <div class="col-12 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8">Event Title : </label>
                <input type="text" class="form-control radius-8" placeholder="Enter Event Title " v-model="editEventData.title" />
              </div>

              <div class="col-md-6 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8" for="editstartDate">Start
                  Date</label>
                <div class="position-relative">
                  <input class="form-control radius-8 bg-base" id="editstartDate" type="text"
                    placeholder="03/12/2024, 10:30 AM" v-model="editEventData.startDate" />
                  <span class="position-absolute end-0 top-50 translate-middle-y me-12 line-height-1">
                    <iconify-icon icon="solar:calendar-linear" class="icon text-lg"></iconify-icon>
                  </span>
                </div>
              </div>

              <div class="col-md-6 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8" for="editendDate">End Date</label>
                <div class="position-relative">
                  <input class="form-control radius-8 bg-base" id="editendDate" type="text"
                    placeholder="03/12/2024, 2:30 PM" v-model="editEventData.endDate" />
                  <span class="position-absolute end-0 top-50 translate-middle-y me-12 line-height-1">
                    <iconify-icon icon="solar:calendar-linear" class="icon text-lg"></iconify-icon>
                  </span>
                </div>
              </div>

              <!-- Label Edit -->
              <div class="col-12 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8">Label</label>
                <div class="d-flex align-items-center flex-wrap gap-28">
                  <div class="form-check checked-success d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="editPersonal" v-model="editEventData.label" value="Personal" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="editPersonal">
                      <span class="w-8-px h-8-px bg-success-600 rounded-circle"></span>
                      Personal
                    </label>
                  </div>
                  <div class="form-check checked-primary d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="editBusiness" v-model="editEventData.label" value="Business" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="editBusiness">
                      <span class="w-8-px h-8-px bg-primary-600 rounded-circle"></span>
                      Business
                    </label>
                  </div>
                  <div class="form-check checked-warning d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="editFamily" v-model="editEventData.label" value="Family" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="editFamily">
                      <span class="w-8-px h-8-px bg-warning-600 rounded-circle"></span>
                      Family
                    </label>
                  </div>
                  <div class="form-check checked-secondary d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="editImportant" v-model="editEventData.label" value="Important" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="editImportant">
                      <span class="w-8-px h-8-px bg-lilac-600 rounded-circle"></span>
                      Important
                    </label>
                  </div>
                  <div class="form-check checked-danger d-flex align-items-center gap-2">
                    <input class="form-check-input" type="radio" name="label" id="editHoliday" v-model="editEventData.label" value="Holiday" />
                    <label
                      class="form-check-label line-height-1 fw-medium text-secondary-light text-sm d-flex align-items-center gap-1"
                      for="editHoliday">
                      <span class="w-8-px h-8-px bg-danger-600 rounded-circle"></span>
                      Holiday
                    </label>
                  </div>
                </div>
              </div>

              <div class="col-12 mb-20">
                <label class="form-label fw-semibold text-primary-light text-sm mb-8" for="editdesc">Description</label>
                <textarea class="form-control" id="editdesc" rows="4" cols="50"
                  placeholder="Write some text" v-model="editEventData.description"></textarea>
              </div>

              <div class="d-flex align-items-center justify-content-center gap-3 mt-24">
                <button type="reset"
                  class="border border-danger-600 bg-hover-danger-200 text-danger-600 text-md px-40 py-11 radius-8">
                  Cancel
                </button>
                <button type="submit" @click="updateEvent" class="btn btn-primary border border-primary-600 text-md px-24 py-12 radius-8">
                  Save
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal Delete Event -->
  <div class="modal fade" id="exampleModalDelete" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-sm modal-dialog modal-dialog-centered">
      <div class="modal-content radius-16 bg-base">
        <div class="modal-body p-24 text-center">
          <span class="mb-16 fs-1 line-height-1 text-danger">
            <iconify-icon icon="fluent:delete-24-regular" class="menu-icon"></iconify-icon>
          </span>
          <h6 class="text-lg fw-semibold text-primary-light mb-0">Are your sure you want to delete this event</h6>
          <div class="d-flex align-items-center justify-content-center gap-3 mt-24">
            <button type="reset"
              class="w-50 border border-danger-600 bg-hover-danger-200 text-danger-600 text-md px-40 py-11 radius-8">
              Cancel
            </button>
            <button type="button" @click="deleteEvent" class="w-50 btn btn-primary border border-primary-600 text-md px-24 py-12 radius-8">
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script setup>
import { ref, onMounted } from 'vue';
import flatpickr from "flatpickr";
import "flatpickr/dist/flatpickr.css";

const events = ref([
  {
    color: 'bg-warning-600',
    time: 'Today, 10:30 PM - 02:30 AM',
    name: 'Design Conference'
  },
  {
    color: 'bg-success-600',
    time: 'Today, 10:30 PM - 02:30 AM',
    name: 'Weekend Festival'
  },
  {
    color: 'bg-info-600',
    time: 'Today, 10:30 PM - 02:30 AM',
    name: 'Design Conference'
  },
  {
    color: 'bg-warning-600',
    time: 'Today, 10:30 PM - 02:30 AM',
    name: 'Ultra Europe 2019'
  },
  {
    color: 'bg-warning-600',
    time: 'Today, 10:30 PM - 02:30 AM',
    name: 'Design Conference'
  }
]);

const eventData = ref({
  title: "",
  startDate: "",
  endDate: "",
  label: "",
  description: "",
});

const editEventData = ref({
  title: "",
  startDate: "",
  endDate: "",
  label: "",
  description: "",
});

const startDate = ref(null);
const endDate = ref(null);

function saveEvent() {
  console.log("Event Saved:", eventData.value);
  // Implementation for saving the event
}

function updateEvent() {
  console.log("Event Updated:", editEventData.value);
  // Implementation for updating the event
}

function deleteEvent() {
  console.log("Event Deleted");
  // Implementation for deleting the event
}

function closeModal() {
  const modal = document.getElementById("exampleModal");
  const bootstrapModal = new bootstrap.Modal(modal);
  bootstrapModal.hide();
}

onMounted(() => {
  flatpickr(startDate.value, {
    enableTime: true,
    dateFormat: "m/d/Y, h:i K",
  });

  flatpickr(endDate.value, {
    enableTime: true,
    dateFormat: "m/d/Y, h:i K",
  });

  const editStart = document.getElementById("editstartDate");
  const editEnd = document.getElementById("editendDate");

  if (editStart) {
    flatpickr(editStart, {
      enableTime: true,
      dateFormat: "m/d/Y, h:i K",
    });
  }

  if (editEnd) {
    flatpickr(editEnd, {
      enableTime: true,
      dateFormat: "m/d/Y, h:i K",
    });
  }
});
</script>