<script>
  import Modal from "./Modal.svelte";

  let fullName = "Zaranik B.U.";
  let group = "IP-01";
  let faculty = "FICT";
  let address = "м. Одеса";
  let telegram = "@t_Zaranik";

  //validators
  let fullNameValid = null;
  let groupValid = null;
  let facultyValid = null;
  let addressValid = null;
  let telegramValid = null;

  let isFullValid = null;



  let showModal = false;

  function toggleModal() {
    showModal = !showModal;
  }

  function handleSubmit() {
    showModal = isFullValid = validate(fullName, group, faculty, address, telegram);
  }

  const validate = (fullName, group, faculty, address, telegram) => {
    fullNameValid = validateFullName(fullName);
    groupValid = validateGroud(group);
    facultyValid = validateFaculty(faculty);
    addressValid = validateAddress(address);
    telegramValid = validateTelegram(telegram);
    return (
      fullNameValid &&
      groupValid &&
      facultyValid &&
      addressValid &&
      telegramValid
    );
  };

  const validateFullName = (fullName) => {
    const regex = /^[\p{L}]* [\p{L}]\.[\p{L}]\.$/u;
    return regex.test(fullName);
  };

  const validateGroud = (group) => {
    const regex = /^[\p{Lu}]{2}-\d{2}$/u;
    return regex.test(group);
  };

  const validateFaculty = (faculty) => {
    const regex = /^\p{Lu}{3,}$/u;
    return regex.test(faculty);
  };

  const validateAddress = (address) => {
    const regex = /^м.\s[\p{Lu}][\p{L}]*$/u;
    return regex.test(address);
  };

  const validateTelegram = (telegram) => {
    const regex = /^@[\p{L}]{1}_[\p{L}]*$/u;
    return regex.test(telegram);
  };

</script>

<div id="form-block">
  <p id="formTitle">Форма для заповнення</p>

  <label for="fullName">ПІБ:</label>
  <input
    placeholder="Прохоренко А.М."
    class:notValidTextInput={fullNameValid != null && !fullNameValid}
    type="text"
    id="fullName"
    bind:value={fullName}
  />

  <label for="group">Група:</label>
  <input
    placeholder="AM-32"
    class:notValidTextInput={groupValid != null && !groupValid}
    type="text"
    id="group"
    bind:value={group}
  />

  <label for="faculty">Факультет:</label>
  <input
    placeholder="ФIОТ"
    class:notValidTextInput={facultyValid != null && !facultyValid}
    type="text"
    id="faculty"
    bind:value={faculty}
  />

  <label for="address">Адреса:</label>
  <input
    placeholder="м. Одеса"
    class:notValidTextInput={addressValid != null && !addressValid}
    type="text"
    id="address"
    bind:value={address}
  />

  <label for="telegram">Telegram-тег:</label>
  <input
    placeholder="@T_TTTTTTT"
    class:notValidTextInput={telegramValid != null && !telegramValid}
    type="text"
    id="telegram"
    bind:value={telegram}
  />

  <button on:click={handleSubmit}>Send</button>
</div>

{#if isFullValid == null}
  <!-- nothing to print -->
{:else if isFullValid === true}
  <Modal show = {showModal}>
    <h3>Everything is ok!</h3>
    <div class="modal-result">
      <p>ПІБ: {fullName}</p>
      <p>Група: {group}</p>
      <p>Факультет: {faculty}</p>
      <p>Адреса: {address}</p>
      <p>Telegram-тег: {telegram}</p>
    </div>
    <button on:click={toggleModal}>Close Modal</button>
  </Modal>
{/if}

<style>
  @import url("https://fonts.googleapis.com/css2?family=Comfortaa:wght@300;700&display=swap");

  * {
    font-family: "Comfortaa", cursive;
  }

  #formTitle {
    font-size: 30px;
  }

  #form-block {
    max-width: 500px;
    margin: 0 auto;
  }

  label {
    display: inline-block;
    margin-top: 10px;
  }

  input[type="text"] {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border-radius: 8px;
  }

  button {
    font-weight: bold;
    margin-top: 20px;
    width: 300px;
    background-color: #007bff;
    color: #fff;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
    border-radius: 8px;
  }

  .notValidTextInput {
    border-color: tomato;
  }

  .modal-result {
    display: flex;
    flex-direction: column;
    align-items: start;
  }
</style>
