<script lang="ts">
    import {Modal, ModalHeader, ModalBody, Navbar, Input, Form, ModalFooter, Button} from "sveltestrap";
  import SelectLanguage from "./SelectLanguage.svelte";
  import Icon from "./Icon.svelte";
    import Dmart, {Status} from "@edraj/tsdmart";
    import {Level, showToast} from "@/utils/toast";

  let openFeedbackModal = false
  let feedback = "";
  let handleOpenFeedbackModal = () => {
      openFeedbackModal = !openFeedbackModal;
  };

  async function handleFormSubmit(event: any) {
    event.preventDefault();
    const response = await Dmart.submit("applications", "feedback", "feedbacks", {feedback});
      if (response.status == Status.success) {
        showToast(Level.info);
        openFeedbackModal = false;
      } else {
        showToast(Level.warn);
      }
  }
</script>

<Modal isOpen={openFeedbackModal} toggle={handleOpenFeedbackModal} centered={true}>
  <ModalHeader>Feedback</ModalHeader>
  <Form on:submit={handleFormSubmit}>
    <ModalBody>
      <p>Let us know how we can improve?</p>
      <Input type="textarea" placeholder="Your feedback" bind:value={feedback} />
    </ModalBody>
    <ModalFooter>
      <Button type="submit" color="primary">Submit</Button>
    </ModalFooter>
  </Form>
</Modal>

<Navbar class="px-3" color="light" light style="border-top: solid #cecece">
  <SelectLanguage />
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div on:click={handleOpenFeedbackModal}>
    <Icon name="envelope" style="cursor: pointer"/>
  </div>
</Navbar>
