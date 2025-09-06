// Highlight active nav link
const navLinks = document.querySelectorAll('.navbar a');
navLinks.forEach(link => {
  link.addEventListener('click', function () {
    navLinks.forEach(el => el.classList.remove('active'));
    this.classList.add('active');
  });
});

// Lightbox functionality
document.querySelectorAll('.gallery .item img').forEach(img => {
  img.style.cursor = 'pointer';
  img.onclick = function () {
    document.getElementById('lightbox-img').src = this.src;
    document.getElementById('lightbox').style.display = 'flex';
  };
});

document.getElementById('lightbox').onclick = function () {
  this.style.display = 'none';
};

// EmailJS for reservation
document.addEventListener("DOMContentLoaded", function () {
  emailjs.init("rGovxfaaOlHc2Biua"); // Your EmailJS public key

  document.getElementById("reservation-form").addEventListener("submit", function (event) {
    event.preventDefault();

    const templateParams = {
      full_name: document.getElementById("full-name").value,
      email: document.getElementById("email").value,
      phone: document.getElementById("phone").value,
      date: document.getElementById("date").value,
      time: document.getElementById("time").value,
      guests: document.getElementById("guests").value,
    };

    emailjs.send("service_f8dajvw", "template_x3s4imo", templateParams)
      .then(function (response) {
        alert("Reservation sent successfully! Thank you.");
      })
      .catch(function (error) {
        alert("Failed to send reservation. Please try again.");
        console.error(error);
      });
  });
});
