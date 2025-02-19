# postcards-from-my-jungle

# Training the Image Model

To train my image model, I first started by downloading the following dataset from the Kaggle website : https://www.kaggle.com/datasets/alessiocorrado99/animals10?resource=download. This dataset contains images of animals from 10 different categories. I then proceeded to use only the first 1024 images, I resized the to be 64 by 64 pixels, I applied a random horizontal flip, a random rotation , and a color jitter so I would get a variation in brightness and contrast. I used a U-Net architecture to generate images from noise. The input/output have 3 channels of RGB images, use 4 blocks each for downsampling and upsampling, and I include attention layers in deeper layers. I define my noise scheduler to be 1000 diffusion steps for the denoisisng process. I decided to use 30 epochs for training the model. Finally, I save the model weight for generating future animal images to animal_diffusion_model.pth.

# Generating Fictional Images of Animals

To generate images, I followed the reverse diffusion process. I begin with random noise, and gradually remove this noise to get in the end each generated image. At first, I load the trained model from earlier (animal_diffusion_model.pth), I move the model to GPU , and set model to evaluation mode. I then proceed to make an output directory called generated_images. To get 50 images, I loop through 50 iterations, and I initialize random noise for each image. I then remove this noise through 1000 steps to reconstruct a clean image (from 999 to 0). Finally, I save each image to generated_images folder in a .zip file.

# Generating Fictional Sounds of Animals

To generate sounds, I import all the necessary libraries including StableAudioPipeline, soundfile ,and Audio. I then proceed to log into my HuggingFace account using
my READ token that I generated from my HuggingFace account which allows me to read from StableAudioPipeline. I then load the Stable Audio Model, and use 16-bit 
floating point precision for faster computation, and I load the model to the GPU. I define 4 unique text promts describing fictional animals, and I specify their sounds and durations. Finally, I generate the audio with promt, a negative promt, num_inference_steps to 200 to define how many steps are used in the diffusion process. The generated audio is saved to a .wav file.

# Generating Fictional Language of Animals

To generate a fictional animal language, I retrieve the OpenAI API Key, and set up my OpenAI APi Client. I then define a structured promt defining fictional world 
where animals communicate with each other via unique phrases, and I ask the model to continue the list of new animal phrases. I set the temperature to 0.7 ensuring a certain degree of randomness, and set the top_p=1.0 to ensure that the response is generated with a higher probability of diversity. I then extract the generated animal phrases and save it as a .txt file in an array.

# How to improve the quality of images and sounds

To improve the quality of images and sounds, I would need to use higher resolution images, optimize the image size , to use a modern image format like WebP and AVIF, I should also use image scaling to make sure they are properly displayed. To improve the quality of sound, I can use hight-quality audio files, use
compression without loss of quality, normalize audio levels, and to loop audio files efficiently to amke sure the sound fades in and out without any transitions.