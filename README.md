<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Student Registration Form</title>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="bg-gray-100 min-h-screen flex items-center justify-center p-4">

  <!-- Registration Form -->
  <div class="bg-white w-full max-w-2xl rounded-2xl shadow-lg p-6 sm:p-8">

    <h1 class="text-3xl font-bold text-center text-blue-600 mb-2">
      Student Registration
    </h1>

    <p class="text-center text-gray-500 mb-8">
      Please fill in the details below
    </p>

    <form id="registrationForm" novalidate>

      <!-- Full Name -->
      <div class="mb-5">
        <label for="name" class="block text-gray-700 font-semibold mb-2">
          Full Name
        </label>

        <input
          type="text"
          id="name"
          placeholder="Enter your full name"
          class="w-full px-4 py-3 border border-gray-300 rounded-lg
                 focus:outline-none focus:ring-2 focus:ring-blue-500"
        >

        <p id="nameError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Email -->
      <div class="mb-5">
        <label for="email" class="block text-gray-700 font-semibold mb-2">
          Email Address
        </label>

        <input
          type="text"
          id="email"
          placeholder="example@email.com"
          class="w-full px-4 py-3 border border-gray-300 rounded-lg
                 focus:outline-none focus:ring-2 focus:ring-blue-500"
        >

        <p id="emailError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Mobile Number -->
      <div class="mb-5">
        <label for="mobile" class="block text-gray-700 font-semibold mb-2">
          Mobile Number
        </label>

        <input
          type="text"
          id="mobile"
          placeholder="Enter 10-digit mobile number"
          maxlength="10"
          class="w-full px-4 py-3 border border-gray-300 rounded-lg
                 focus:outline-none focus:ring-2 focus:ring-blue-500"
        >

        <p id="mobileError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Course -->
      <div class="mb-5">
        <label for="course" class="block text-gray-700 font-semibold mb-2">
          Select Course
        </label>

        <select
          id="course"
          class="w-full px-4 py-3 border border-gray-300 rounded-lg
                 focus:outline-none focus:ring-2 focus:ring-blue-500"
        >
          <option value="">-- Select Course --</option>
          <option value="BCA">BCA</option>
          <option value="BBA">BBA</option>
          <option value="BSc">B.Sc</option>
          <option value="BCom">B.Com</option>
          <option value="BA">B.A</option>
        </select>

        <p id="courseError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Password -->
      <div class="mb-5">
        <label for="password" class="block text-gray-700 font-semibold mb-2">
          Password
        </label>

        <input
          type="password"
          id="password"
          placeholder="Minimum 8 characters"
          class="w-full px-4 py-3 border border-gray-300 rounded-lg
                 focus:outline-none focus:ring-2 focus:ring-blue-500"
        >

        <p id="passwordError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Confirm Password -->
      <div class="mb-5">
        <label
          for="confirmPassword"
          class="block text-gray-700 font-semibold mb-2"
        >
          Confirm Password
        </label>

        <input
          type="password"
          id="confirmPassword"
          placeholder="Re-enter your password"
          class="w-full px-4 py-3 border border-gray-300 rounded-lg
                 focus:outline-none focus:ring-2 focus:ring-blue-500"
        >

        <p id="confirmPasswordError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Terms -->
      <div class="mb-6">
        <label class="flex items-start gap-3">
          <input
            type="checkbox"
            id="terms"
            class="mt-1 w-4 h-4 accent-blue-600"
          >

          <span class="text-gray-600 text-sm">
            I agree to the terms and conditions.
          </span>
        </label>

        <p id="termsError" class="text-red-500 text-sm mt-1"></p>
      </div>


      <!-- Submit Button -->
      <button
        type="submit"
        class="w-full bg-blue-600 text-white py-3 rounded-lg
               font-semibold text-lg hover:bg-blue-700
               transition duration-200"
      >
        Register
      </button>


      <!-- Success Message -->
      <div
        id="successMessage"
        class="hidden mt-5 p-4 bg-green-100 border
               border-green-400 text-green-700 rounded-lg text-center"
      >
        Registration successful!
      </div>

    </form>
  </div>


  <!-- JavaScript Validation -->
  <script>

    const form = document.getElementById("registrationForm");

    form.addEventListener("submit", function(event) {

      // Prevent form submission
      event.preventDefault();

      // Get values
      const name = document.getElementById("name").value.trim();
      const email = document.getElementById("email").value.trim();
      const mobile = document.getElementById("mobile").value.trim();
      const course = document.getElementById("course").value;
      const password = document.getElementById("password").value;
      const confirmPassword =
        document.getElementById("confirmPassword").value;
      const terms = document.getElementById("terms").checked;

      // Error elements
      const nameError = document.getElementById("nameError");
      const emailError = document.getElementById("emailError");
      const mobileError = document.getElementById("mobileError");
      const courseError = document.getElementById("courseError");
      const passwordError = document.getElementById("passwordError");
      const confirmPasswordError =
        document.getElementById("confirmPasswordError");
      const termsError = document.getElementById("termsError");

      const successMessage =
        document.getElementById("successMessage");

      // Clear previous errors
      nameError.textContent = "";
      emailError.textContent = "";
      mobileError.textContent = "";
      courseError.textContent = "";
      passwordError.textContent = "";
      confirmPasswordError.textContent = "";
      termsError.textContent = "";

      successMessage.classList.add("hidden");

      let isValid = true;


      // -------------------------
      // Name Validation
      // -------------------------

      if (name === "") {
        nameError.textContent = "Full name is required.";
        isValid = false;
      }


      // -------------------------
      // Email Validation
      // -------------------------

      const emailPattern =
        /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

      if (email === "") {

        emailError.textContent =
          "Email address is required.";

        isValid = false;

      } else if (!emailPattern.test(email)) {

        emailError.textContent =
          "Please enter a valid email address.";

        isValid = false;
      }


      // -------------------------
      // Mobile Validation
      // -------------------------

      const mobilePattern = /^[0-9]{10}$/;

      if (mobile === "") {

        mobileError.textContent =
          "Mobile number is required.";

        isValid = false;

      } else if (!mobilePattern.test(mobile)) {

        mobileError.textContent =
          "Mobile number must contain exactly 10 digits.";

        isValid = false;
      }


      // -------------------------
      // Course Validation
      // -------------------------

      if (course === "") {

        courseError.textContent =
          "Please select a course.";

        isValid = false;
      }


      // -------------------------
      // Password Validation
      // -------------------------

      if (password === "") {

        passwordError.textContent =
          "Password is required.";

        isValid = false;

      } else if (password.length < 8) {

        passwordError.textContent =
          "Password must be at least 8 characters.";

        isValid = false;
      }


      // -------------------------
      // Confirm Password
      // -------------------------

      if (confirmPassword === "") {

        confirmPasswordError.textContent =
          "Please confirm your password.";

        isValid = false;

      } else if (password !== confirmPassword) {

        confirmPasswordError.textContent =
          "Passwords do not match.";

        isValid = false;
      }


      // -------------------------
      // Terms Validation
      // -------------------------

      if (!terms) {

        termsError.textContent =
          "You must agree to the terms and conditions.";

        isValid = false;
      }


      // -------------------------
      // Final Result
      // -------------------------

      if (isValid) {

        successMessage.classList.remove("hidden");

        // Reset form
        form.reset();

      }

    });

  </script>

</body>
</html>
