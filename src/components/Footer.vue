<template>
    <footer class="container">
        <div>
            <p>I’m always looking for new opportunities, <a href="mailto:mdassignies@gmail.com" @click="fbTrack">contact me</a> ! </p>
        </div>
        <div class="icons">
            <a href="https://twitter.com/digitalsailor_" target="_blank">
                <svg width="19" height="17" viewBox="0 0 19 17" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M5.07982 16C8.06723 16.0999 10.9681 14.9876 13.1227 12.9158C15.2773 10.844 16.5026 7.98901 16.5198 4.99999C17.1975 4.1614 17.7007 3.19581 17.9998 2.15999C18.0454 1.99281 17.9887 1.81443 17.8549 1.70435C17.721 1.59427 17.5351 1.57298 17.3798 1.64999C16.6529 1.99991 15.7837 1.847 15.2198 1.26999C14.5106 0.493317 13.5171 0.0369476 12.4658 0.00491907C11.4145 -0.0271095 10.395 0.367933 9.63982 1.09999C8.59878 2.10818 8.16235 3.58826 8.48982 4.99999C5.13982 5.19999 2.83982 3.60999 0.999819 1.42999C0.886869 1.30207 0.708969 1.25306 0.546445 1.30506C0.38392 1.35707 0.267527 1.50026 0.249819 1.66999C-0.468064 5.65215 1.36669 9.66068 4.84982 11.72C3.70946 13.0278 2.10803 13.8446 0.379819 14C0.189999 14.0315 0.0411958 14.1801 0.00956334 14.3699C-0.0220691 14.5597 0.0704694 14.7486 0.239819 14.84C1.74334 15.5914 3.39905 15.9882 5.07982 16"
                        fill="#151725" />
                </svg>
            </a>
            <a href="https://www.linkedin.com/in/marin-d-assignies-77a741153/" target="_blank">
                <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M12.1498 5.4C10.6019 5.39469 9.11535 6.0052 8.01797 7.09695C6.9206 8.1887 6.30245 9.67205 6.2998 11.22V17.1C6.2998 17.3387 6.39463 17.5676 6.56341 17.7364C6.73219 17.9052 6.96111 18 7.1998 18H9.2998C9.79686 18 10.1998 17.5971 10.1998 17.1V11.22C10.1994 10.6687 10.4336 10.1432 10.8439 9.77494C11.2541 9.40665 11.8017 9.23032 12.3498 9.29C13.3558 9.4167 14.1078 10.2761 14.0998 11.29V17.1C14.0998 17.5971 14.5027 18 14.9998 18H17.0998C17.5969 18 17.9998 17.5971 17.9998 17.1V11.22C17.9972 9.67205 17.379 8.1887 16.2816 7.09695C15.1843 6.0052 13.6977 5.39469 12.1498 5.4V5.4Z"
                        fill="#151725" />
                    <rect y="6.29999" width="4.5" height="11.7" rx="0.9" fill="#151725" />
                    <path
                        d="M2.25 4.5C3.49264 4.5 4.5 3.49264 4.5 2.25C4.5 1.00736 3.49264 0 2.25 0C1.00736 0 0 1.00736 0 2.25C0 3.49264 1.00736 4.5 2.25 4.5Z"
                        fill="#151725" />
                </svg>
            </a>
        </div>
    </footer>
</template>

<script>
    export default {
        name: 'Footer',
        
        methods: {
            fbTrack () {
                window.fbq('track', 'Contact');
                console.log('tracking');
            }
        },
    }
</script>

<style lang="scss" scoped>

footer{
    display: flex;
    justify-content: space-between;
    background-color: white;
    padding-bottom: 1rem;
    padding-top: 1rem;
    height: 8vh;
    @media screen and (max-width: 800px){
        height: auto;
    }
}

p{
    margin-bottom: 0;
}

a{
    color: inherit;
    
}


.icons a {
    margin-left: 1rem;
}
</style>