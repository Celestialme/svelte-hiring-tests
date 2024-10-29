<script lang="ts">
  // TODO: Implement form state management
  // TODO: Implement form validation
  // TODO: Implement submit handler
  // TODO: Implement success state management
  let fields: App.UserFormData = {
    email: "",
    firstName: "",
    lastName: "",
    password: "",
  };
  let errors: App.UserFormData = {
    email: "",
    firstName: "",
    lastName: "",
    password: "",
  };
  let submitted = false;
  let data: App.UserFormData;
  function onsubmit() {
    submitted = true;
    errors = {
      email: "",
      firstName: "",
      lastName: "",
      password: "",
    };
    data = fields;
    fields = {
      email: "",
      firstName: "",
      lastName: "",
      password: "",
    };
  }

  function validateEmail({ target }: Event) {
    let email = (target as HTMLInputElement).value;

    if (!email) errors.email = "Email is required";
    else if (!email.includes("@")) errors.email = "Email must include @ character";
    else errors.email = "Email should be in valid format";
  }

  function validatePassword({ target }: Event) {
    let password = (target as HTMLInputElement).value;
    if (!password) errors.password = "Password is required";
    else if (password.length < 6) errors.password = "Password must be at least 6 characters";
  }
</script>

<div class="form-container">
  <form on:submit={onsubmit}>
    <div class="form-group">
      <label for="firstName">First Name</label>
      <input class:error={errors.firstName} on:input={() => ((errors.firstName = ""), (submitted = false))} bind:value={fields.firstName} id="firstName" type="text" placeholder="Enter your first name" required on:invalid|preventDefault={() => (errors.firstName = "First name is required")} />
      {#if errors.firstName}
        <p class="error-message">
          {errors.firstName}
        </p>
      {/if}
    </div>

    <div class="form-group">
      <label for="lastName">Last Name</label>
      <input class:error={errors.lastName} on:input={() => ((errors.lastName = ""), (submitted = false))} bind:value={fields.lastName} id="lastName" type="text" placeholder="Enter your last name" required on:invalid|preventDefault={() => (errors.lastName = "Last name is required")} />
      {#if errors.lastName}
        <p class="error-message">
          {errors.lastName}
        </p>
      {/if}
    </div>

    <div class="form-group">
      <label for="email">Email</label>
      <input class:error={errors.email} on:input={() => ((errors.email = ""), (submitted = false))} bind:value={fields.email} id="email" type="email" placeholder="Enter your email" required on:invalid|preventDefault={validateEmail} />
      {#if errors.email}
        <p class="error-message">
          {errors.email}
        </p>
      {/if}
    </div>

    <div class="form-group">
      <label for="password">Password</label>
      <input class:error={errors.password} on:input={() => ((errors.password = ""), (submitted = false))} bind:value={fields.password} id="password" type="password" placeholder="Enter your password" required minlength="6" on:invalid|preventDefault={validatePassword} />
      {#if errors.password}
        <p class="error-message">
          {errors.password}
        </p>
      {/if}
    </div>

    <button type="submit" class="submit-button">Submit</button>
  </form>
  {#if submitted}
    <p class="success-message">Form has been successfully submitted</p>
    <p>
      submitted data: first name: {data.firstName}
    </p>
    <p>
      last name: {data.lastName}
    </p>
    <p>
      email: {data.email}
    </p>
  {/if}

  <!-- TODO: Add success message section here -->
</div>

<style>
  .form-container {
    max-width: 480px;
    margin: 0 auto;
    padding: 2rem;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .form-group {
    margin-bottom: 1.5rem;
  }

  label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 500;
    color: #374151;
  }

  input {
    width: 100%;
    padding: 0.75rem;
    border: 1px solid #d1d5db;
    border-radius: 6px;
    font-size: 1rem;
    transition: border-color 0.15s ease-in-out;
  }

  input:focus {
    outline: none;
    border-color: #3b82f6;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
  }

  input::placeholder {
    color: #9ca3af;
  }

  input.error {
    border-color: #ef4444;
  }

  .error-message {
    display: block;
    margin-top: 0.5rem;
    font-size: 0.875rem;
    color: #ef4444;
  }

  .submit-button {
    width: 100%;
    padding: 0.75rem 1.5rem;
    background-color: #3b82f6;
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 1rem;
    font-weight: 500;
    cursor: pointer;
    transition: background-color 0.15s ease-in-out;
  }

  .submit-button:hover {
    background-color: #2563eb;
  }

  .submit-button:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.5);
  }

  .submit-button:disabled {
    background-color: #9ca3af;
    cursor: not-allowed;
  }

  .success-message {
    margin-top: 1.5rem;
    padding: 1rem;
    background-color: #edf7ed;
    border: 1px solid #c8e6c9;
    border-radius: 6px;
    color: #1b5e20;
  }
</style>
