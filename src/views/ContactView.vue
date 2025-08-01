
<template>
  <div class="contact container">
    <h1>Contact</h1>
    <p>
      all enquiries
    </p>
    <a href="mailto:joey@halffullmgmt" target="_blank" alt="Mail" aria-label="Mail" >joey@halffullmgmt.com
      </a>

    <div class="contact_icons">
      <a class="contact_icon instagram" href="http://instagram.com/tslleach" target="_blank" alt="instagram-icon">
        <svg width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M9.75 2.5H20.25C24.25 2.5 27.5 5.75 27.5 9.75V20.25C27.5 22.1728 26.7362 24.0169 25.3765 25.3765C24.0169 26.7362 22.1728 27.5 20.25 27.5H9.75C5.75 27.5 2.5 24.25 2.5 20.25V9.75C2.5 7.82718 3.26384 5.98311 4.62348 4.62348C5.98311 3.26384 7.82718 2.5 9.75 2.5ZM9.5 5C8.30653 5 7.16193 5.47411 6.31802 6.31802C5.47411 7.16193 5 8.30653 5 9.5V20.5C5 22.9875 7.0125 25 9.5 25H20.5C21.6935 25 22.8381 24.5259 23.682 23.682C24.5259 22.8381 25 21.6935 25 20.5V9.5C25 7.0125 22.9875 5 20.5 5H9.5ZM21.5625 6.875C21.9769 6.875 22.3743 7.03962 22.6674 7.33265C22.9604 7.62567 23.125 8.0231 23.125 8.4375C23.125 8.8519 22.9604 9.24933 22.6674 9.54235C22.3743 9.83538 21.9769 10 21.5625 10C21.1481 10 20.7507 9.83538 20.4576 9.54235C20.1646 9.24933 20 8.8519 20 8.4375C20 8.0231 20.1646 7.62567 20.4576 7.33265C20.7507 7.03962 21.1481 6.875 21.5625 6.875ZM15 8.75C16.6576 8.75 18.2473 9.40848 19.4194 10.5806C20.5915 11.7527 21.25 13.3424 21.25 15C21.25 16.6576 20.5915 18.2473 19.4194 19.4194C18.2473 20.5915 16.6576 21.25 15 21.25C13.3424 21.25 11.7527 20.5915 10.5806 19.4194C9.40848 18.2473 8.75 16.6576 8.75 15C8.75 13.3424 9.40848 11.7527 10.5806 10.5806C11.7527 9.40848 13.3424 8.75 15 8.75ZM15 11.25C14.0054 11.25 13.0516 11.6451 12.3483 12.3483C11.6451 13.0516 11.25 14.0054 11.25 15C11.25 15.9946 11.6451 16.9484 12.3483 17.6517C13.0516 18.3549 14.0054 18.75 15 18.75C15.9946 18.75 16.9484 18.3549 17.6517 17.6517C18.3549 16.9484 18.75 15.9946 18.75 15C18.75 14.0054 18.3549 13.0516 17.6517 12.3483C16.9484 11.6451 15.9946 11.25 15 11.25Z" fill="white"/>
        </svg> 
      </a>
      <a class="contact_icon mail" href="mailto:joey@halffullmgmt" target="_blank" alt="Mail" aria-label="Mail">
        <svg width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path opacity="0" d="M25 10L15 16.25L5 10V22.5H25V10ZM25 7.5H5L15 13.7375L25 7.5Z" fill="#ffffff"/>
          <path d="M5 25H25C26.375 25 27.5 23.875 27.5 22.5V7.5C27.5 6.125 26.375 5 25 5H5C3.625 5 2.5 6.125 2.5 7.5V22.5C2.5 23.875 3.625 25 5 25ZM25 7.5L15 13.7375L5 7.5H25ZM5 10L15 16.25L25 10V22.5H5V10Z" fill="#ffffff"/>
        </svg>
      </a>
    </div>
  </div>
</template>

<style>
 .contact {
    text-align: center;
    height: 100dvh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    max-width: 670px;
    margin: 0 auto;
    padding: 2rem;
 }

 .contact_icons {
  display: flex;
  gap: 1rem;
  place-items: center;
  justify-content: center;
  align-items: center;
  margin-top: 2rem;
 }

 .contact_icon {
  height: 30px;
  width: 30px;
  transition-duration: 0.3s;
 }

a.contact_icon path {
  fill: #ffffff;
  transition-duration: 0.3s;
}

a.contact_icon.mail:hover path,
a.contact_icon.instagram:hover path {
  fill: #EA4335;
  transition-duration: 0.3s;
}

a.contact_icon.twitter:hover path {
  fill: #1C9BEF;
  transition-duration: 0.3s;
}

.contact a {
  display: inline-block;
  transition: transform 0.3s ease-out;
  color: #1C9BEF;
  text-decoration: none;
  will-change: transform;
}

@media screen and (min-width: 768px) {

  .contact a:hover {
    transition: transform 0.3s ease-out;
    transform: scale(1.1);
  }
    
}


</style>
