<template>
    <div class="fade-right">
        <h2>Sign In.</h2>
        <p>You are current not logged in. Please login to see your ETH wallet value & ethosOS rig stats.</p>
        <div :class="{ 'disabled' : submited }">
            <section>
                <label>Email</label>
                <input type="text" placeholder="name@domain.com" v-model="form.email">
                <label>Password</label>
                <div class="input-icon-right">
                    <input :type="viewPassword ? 'text' : 'password'" placeholder="password" v-model="form.password">
                    <span @click="viewPassword = !viewPassword" class="material-icons">{{ viewPassword ? 'visibility' : 'visibility_off' }}</span>
                </div>
                <router-link to="/authenticate/resetPassword"><a id="forgot-password">forgot password?</a></router-link>
            </section>
            <section>
                <button @click="Login" class="btn-action large">Sign In</button>
                <p>Don't have an account yet? <router-link to="/authenticate/register"><a>Sign up</a></router-link>.</p>
            </section>
        </div>
    </div>
</template>

<script>
export default {
    emits: ['submit', 'success', 'error'],
    data() {
        return {
            submited: false,
            viewPassword: false,
            form: {
                email: '',
                password: ''
            }
        }
    },
    methods: {
        Login: async function() {
            this.submited = true;
            this.$emit('submit', true);
            await setTimeout(() => {
                this.$store.dispatch('LOGIN', this.form)
                    .then(() => this.$emit('success'))
                    .catch(err => {
                        this.submited = false;
                        this.$emit('error', err.response.data.error);
                    });
            }, 1000);
        }
    },
}
</script>

<style lang="scss" scoped>
    
    #forgot-password {
        float: right;
        font-size: 14px;
        right: 0;
        margin-bottom: 20px;
    }

</style>