<template>
    <div class="container">
        <div class="column">
            <div class="column">
                <div class="message" v-for="status in statuses">
                    <div class="message-header">
                        <p>
                            {{ status.user.name }} said
                        </p>
                        <p>
                            <!-- vue filters instead of postedOn method -->
                            {{ status.created_at | ago | capitalize }}
                        </p>
                    </div>

                    <div class="message-body" v-text="status.body"></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import moment from 'moment';
import Status from '../models/Status';

export default {
    data() {
        return {
            statuses: []
        }
    },
    created() {
        Status.all( statuses => this.statuses = statuses);
    },

    filters: {
        ago(date) {
            return moment(date).fromNow();
        },
        capitalize(value) {
            return value.toUpperCase();
        }
    }

}
</script>
