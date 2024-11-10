            ctx.moveTo(0, 125);
            ctx.lineTo(250, 125);
            ctx.stroke();
        }

        function startNewQuestion() {
            // Randomly pick a question that has not been asked
            let randomIndex = Math.floor(Math.random() * questions.length);
            while (askedQuestions.includes(randomIndex)) {
                randomIndex = Math.floor(Math.random() * questions.length);
            }

            currentQuestion = questions[randomIndex];
            askedQuestions.push(randomIndex);
            // Draw the question
            ctx.clearRect(0, 0, 250, 250);  // Clear canvas
            currentQuestion.draw(ctx);
            document.getElementById('questionText').innerText = currentQuestion.question;
            // Set the choices
            let choices = currentQuestion.choices;
            document.getElementById('choice1').innerText = choices[0];
            document.getElementById('choice2').innerText = choices[1];
            document.getElementById('choice3').innerText = choices[2];
            document.getElementById('choice4').innerText = choices[3];
            document.getElementById('feedback').style.opacity = 0; // Hide feedback
        }

        function checkAnswer(choiceIndex) {
            const chosenAnswer = document.getElementById(`choice${choiceIndex + 1}`).innerText;
            const correctAnswer = currentQuestion.correctAnswer;

            const feedbackElement = document.getElementById('feedback');
            if (chosenAnswer === correctAnswer) {
                feedbackElement.innerText = "إجابة صحيحة!";
                feedbackElement.style.color = "#4CAF50";
                score += 10;  // Increase score
            } else {
                feedbackElement.innerText = "إجابة خاطئة!";
                feedbackElement.style.color = "#d9534f";
            }

            document.getElementById('score').innerText = `النقاط: ${score}`;

            // Show feedback and move to the next question after 2 seconds
            feedbackElement.style.opacity = 1;
            setTimeout(() => {
                if (askedQuestions.length < questions.length) {
                    startNewQuestion();  // Start new question if there are more questions
                } else {
                    feedbackElement.innerText = "لقد أكملت جميع الأسئلة!";
                }
            }, 2000);
        }

        // Initialize the game by showing the first question
        startNewQuestion();
    </script>
</body>
</html>

