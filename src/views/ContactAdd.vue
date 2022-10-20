<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="onAddContact"/>
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import { contactService } from '@/services/contact.service';
export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                    name: '',
                    email: '',
                    address: '',
                    phone: '',
                    favorite: 0
            },
            message: '',
        };
    },
    methods: {
        async onAddContact(contact) {
            try {
                await contactService.create(contact);
                this.message = 'Liên hệ được tạo thành công.';
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.contact = {name: '',
                        email: '',
                        address: '',
                        phone: '',
                        favorite: null};
        this.message = '';
    },
};
</script>