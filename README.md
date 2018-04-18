# tensorflow_API_explained

1 > 
    string_input_producer :- 

    # Make a queue of file names including all the images specified.
    # Output strings (e.g. filenames) to a queue for an input pipeline.
    
    original_image_list = ["./file1.jpg", "./file2.jpg"]
    filename_queue = tf.train.string_input_producer(original_image_list)
    
2 > 
    Coordinate the loading of image files.
    coord = tf.train.Coordinator()
    threads = tf.train.start_queue_runners(sess=sess, coord=coord)
    
    QueueRunner: When TensorFlow is reading the input, it needs to maintain multiple queues for it. The queue serves all the                    workers that are responsible for executing the training step. We use a queue because we want to have the                      inputs ready for the workers to operate on. If you don't have a queue, you will be blocked on I/O and                          performance will degrade.
    
    Coordindator: This is part of tf.train.Supervisor. It's necessary because you need a controller to maintain the set of                       threads (know when main thread should terminate, request stopping of sub-threads, etc).
    
3 >
    # Read a whole file from the queue, the first returned value in the tuple is the
        # filename which we are ignoring.
        _, image_file = image_reader.read(filename_queue)

        # Decode the image as a JPEG file, this will turn it into a Tensor which we can
        # then use in training.
        image = tf.image.decode_jpeg(image_file)

        # Get a tensor of resized images.
        image = tf.image.resize_images(image, [224, 224])
        image.set_shape((224, 224, 3))


  
