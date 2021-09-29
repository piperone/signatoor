<template>
    <div class="q-pa-xl">
        <h3>I work beautifully:</h3>

        <q-card>
            <q-card-section class="q-pa-none">
                <VPerfectSignature :stroke-options="strokeOptions"
                                   ref="pagePad"
                                   height="400px" />
            </q-card-section>
        </q-card>

        <q-btn color="primary"
               class="full-width q-mt-lg"
               size="lg"
               @click="showDialog = !showDialog"
               label="Show Dialog" />
    </div>

    <q-dialog v-model="showDialog" class="q-pa-lg" full-height full-width>
        <q-card class="q-pa-lg">
            <h3 class="q-mt-none">But I don't :-(</h3>

            <q-btn @click="showDialog = false"
                   icon="close"
                   round
                   class="absolute-top-right q-ma-sm"
                   color="negative" />

            <q-card-section>
                I'm supposed to be in here
                <VPerfectSignature :stroke-options="strokeOptions"
                                   ref="dialogPad"
                                   height="400px" />
            </q-card-section>
        </q-card>
    </q-dialog>
</template>

<script>
import VPerfectSignature from 'v-perfect-signature';

export default {
    name: 'Index',
    components: { VPerfectSignature },

    mounted() {
        window.addEventListener('resize', () => {
            // Shouldn't this resize the canvas after window resize?
            this.$refs.pagePad.resizeCanvas(false);

            // Resizing the window results in the contents of canvas turning
            // invisible until the next mousedown event. The canvas size remains
            // the same as before the resize.
        });
    },

    data() {
        return {
            showDialog: false,
            strokeOptions: {
                size: 16,
                thinning: 0.75,
                smoothing: 0.5,
                streamline: 0.5
            }
        }
    }
}
</script>

<style lang="sass">
.pagePadCard
    height: 400px

.bordered
    border: 1px solid #333
</style>
