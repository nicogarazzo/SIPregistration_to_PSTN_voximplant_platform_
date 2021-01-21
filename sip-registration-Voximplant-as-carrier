let call1, call2, data;

VoxEngine.addEventListener(AppEvents.CallAlerting, (e) => {
  e.call.answer(); // answer incoming call
  call2 = e.call;
  e.call.addEventListener(CallEvents.Connected, handleScenarioStart);
  e.call.addEventListener(CallEvents.Disconnected, () => VoxEngine.terminate());
  //data = "+51978159897";
  data = e.destination;
  call2.say('Dame un momento...', Language.US_SPANISH_FEMALE);
}); 


const callerId = "19075196897"; // Rented or verified phone number

function handleScenarioStart(e) {

  // start scenario - calling number over SIP
  call1 = VoxEngine.callPSTN(data,'19075196897');
  // assign event handlers
  call1.addEventListener(CallEvents.Connected, handleCall2Connected);
  call1.addEventListener(CallEvents.Failed, function (e) {
    call2.say('Llamada ha fallado', Language.US_SPANISH_FEMALE);
    VoxEngine.terminate();
    Logger.write('Llamada fallida - Sesión terminada');
  });
  call1.addEventListener(CallEvents.Disconnected, function (e) {
    call2.say('Llamada desconectada', Language.US_SPANISH_FEMALE);
    VoxEngine.terminate();
  });
}

function handleCall1Connected(e) {
  // first call connected successfully, play message
  
  call2.say('Te conectare ahora con el cliente', Language.US_SPANISH_FEMALE);
  call2.addEventListener(CallEvents.PlaybackFinished, handleCall2Connected);
  
}

function handleCall2Connected(e) {
  // connect two calls with each other - media 
  VoxEngine.sendMediaBetween(call1, call2);
  // and signalling
  VoxEngine.easyProcess(call1, call2);
}
