<template>
  <div>
    <MainSlider subheading="Contact" image="/images/bg_1.jpg" size="small" />

    <section class="ftco-section contact-section">
      <div class="container mt-5">
        <div class="row block-9">
          <div class="col-md-4 contact-info">
            <div class="row">
              <div class="col-md-12 mb-4">
                <h2 class="h4">Contact Information</h2>
              </div>
              <div class="col-md-12 mb-3">
                <p>
                  <span>Address:</span> 198 West 21th Street, Suite 721 New York NY 10016
                </p>
              </div>
              <div class="col-md-12 mb-3">
                <p>
                  <span>Phone:</span>
                  <a href="tel://1234567920">+ 1235 2355 98</a>
                </p>
              </div>
              <div class="col-md-12 mb-3">
                <p>
                  <span>Email:</span>
                  <a href="mailto:info@yoursite.com">info@yoursite.com</a>
                </p>
              </div>
              <div class="col-md-12 mb-3">
                <p>
                  <span>Website:</span>
                  <a href="#">yoursite.com</a>
                </p>
              </div>
            </div>
          </div>
          <div class="col-md-1"></div>
          <div class="col-md-6">
            <form action="#" class="contact-form">
              <div class="row">
                <div class="col-md-6">
                  <div class="form-group">
                    <input type="text" v-model="name" class="form-control" placeholder="Your Name" />
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="form-group">
                    <input
                      type="email"
                      v-model="email"
                      class="form-control"
                      placeholder="Your Email"
                    />
                  </div>
                </div>
              </div>
              <div class="form-group">
                <input type="text" v-model="subject" class="form-control" placeholder="Subject" />
              </div>
              <div class="form-group">
                <textarea
                  name
                  id
                  cols="30"
                  rows="7"
                  v-model="message"
                  class="form-control"
                  placeholder="Message"
                ></textarea>
              </div>
              <div class="form-group">
                <input
                  type="submit"
                  value="Send Message"
                  class="btn btn-primary py-3 px-5"
                  @click.prevent="sendContactMessage"
                />
              </div>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import MainSlider from "@/components/MainSlider";
import { ContactsRef } from "@/modules/firebase";

export default {
  name: "ContactPage",
  components: {
    MainSlider
  },
  data() {
    return {
      name: "",
      email: "",
      subject: "",
      message: ""
    };
  },
  methods: {
    async sendContactMessage() {
        let contactData = {
            name: this.name,
            email: this.email,
            subject: this.subject,
            message: this.message,
            created_at: new Date()
        }

      await ContactsRef.add(contactData)

      alert('Tu contacto ha sido enviado. Te responderemos en un máximo de 24h laborales')
      setTimeout(() => {
          this.$router.go(0)
      },2000)
    }
  }
};
</script>