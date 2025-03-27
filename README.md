stm32f1xx_it.c :

/* USER CODE BEGIN EV */
extern sr04_t sr04_1;
extern sr04_t sr04_2;
extern sr04_t sr04_3;
/* USER CODE END EV */

void TIM1_UP_IRQHandler(void)
{
  /* USER CODE BEGIN TIM1_UP_IRQn 0 */
	// Update interrupt handling
	  if (__HAL_TIM_GET_FLAG(sr04_1.echo_htim, TIM_FLAG_UPDATE) != RESET)
	  {
	      if (__HAL_TIM_GET_IT_SOURCE(sr04_1.echo_htim, TIM_IT_UPDATE) != RESET)
	      {
	          sr04_1.tim_update_count++;
	      }
	  }
	  if (__HAL_TIM_GET_FLAG(sr04_2.echo_htim, TIM_FLAG_UPDATE) != RESET)
	  	  {
	  	      if (__HAL_TIM_GET_IT_SOURCE(sr04_2.echo_htim, TIM_IT_UPDATE) != RESET)
	  	      {
	  	          sr04_2.tim_update_count++;
	  	      }
	  	  }
	  if (__HAL_TIM_GET_FLAG(sr04_3.echo_htim, TIM_FLAG_UPDATE) != RESET)
		  	  {
		  	      if (__HAL_TIM_GET_IT_SOURCE(sr04_3.echo_htim, TIM_IT_UPDATE) != RESET)
		  	      {
		  	          sr04_3.tim_update_count++;
		  	      }
		  	  }
  /* USER CODE END TIM1_UP_IRQn 0 */
  HAL_TIM_IRQHandler(&htim1);
  /* USER CODE BEGIN TIM1_UP_IRQn 1 */

  /* USER CODE END TIM1_UP_IRQn 1 */
}

void TIM1_CC_IRQHandler(void)
{
  /* USER CODE BEGIN TIM1_CC_IRQn 0 */
	 // Capture interrupt handling
		  if (__HAL_TIM_GET_FLAG(&htim1, TIM_FLAG_CC1) != RESET)
		  {
		      if (__HAL_TIM_GET_IT_SOURCE(&htim1, TIM_IT_CC1) != RESET)
		      {
		          sr04_read_distance(&sr04_1);
		      }
		  }
		  if (__HAL_TIM_GET_FLAG(&htim1, TIM_FLAG_CC4) != RESET)
		 	  {
		 	      if (__HAL_TIM_GET_IT_SOURCE(&htim1, TIM_IT_CC4) != RESET)
		 	      {
		 	          sr04_read_distance(&sr04_2);
		 	      }
		 	  }
		  if (__HAL_TIM_GET_FLAG(&htim1, TIM_FLAG_CC3) != RESET)
			 	  {
			 	      if (__HAL_TIM_GET_IT_SOURCE(&htim1, TIM_IT_CC3) != RESET)
			 	      {
			 	          sr04_read_distance(&sr04_3);
			 	      }
			 	  }
  /* USER CODE END TIM1_CC_IRQn 0 */
  HAL_TIM_IRQHandler(&htim1);
  /* USER CODE BEGIN TIM1_CC_IRQn 1 */

  /* USER CODE END TIM1_CC_IRQn 1 */
}

main.c
/* USER CODE BEGIN PV */
sr04_t sr04_1;
sr04_t sr04_2;
sr04_t sr04_3;
/* USER CODE END PV */ 
/* USER CODE BEGIN 2 */
sr04_1.trig_port = GPIOB;
  sr04_1.trig_pin = GPIO_PIN_15;
  sr04_1.echo_htim = &htim1;
  sr04_1.echo_channel = TIM_CHANNEL_1;
  sr04_init(&sr04_1);
  sr04_2.trig_port = GPIOA;
  sr04_2.trig_pin = GPIO_PIN_9;
  sr04_2.echo_htim = &htim1;
  sr04_2.echo_channel = TIM_CHANNEL_4;
  sr04_init(&sr04_2);
  sr04_3.trig_port = GPIOA;
  sr04_3.trig_pin = GPIO_PIN_12;
  sr04_3.echo_htim = &htim1;
  sr04_3.echo_channel = TIM_CHANNEL_3;
  sr04_init(&sr04_3);
	
 /* USER CODE BEGIN WHILE */
  while (1)
  {
	  sr04_trigger(&sr04_1);
	     HAL_Delay(100);
	  sr04_trigger(&sr04_2);
	  	  HAL_Delay(100);
	  sr04_trigger(&sr04_3);
	  	  HAL_Delay(100);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
