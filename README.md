# onlinequizproject
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Class to represent a quiz question
class Question {
    private String questionText;
    private String[] options;
    private int correctAnswer;

    public Question(String questionText, String[] options, int correctAnswer) {
        this.questionText = questionText;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestionText() {
        return questionText;
    }

    public String[] getOptions() {
        return options;
    }

    public int getCorrectAnswer() {
        return correctAnswer;
    }

    public boolean isCorrect(int userAnswer) {
        return userAnswer == correctAnswer;
    }
}

// Class to manage a collection of questions
class Quiz {
    private List<Question> questions;

    public Quiz() {
        questions = new ArrayList<>();
    }

    public void addQuestion(Question question) {
        questions.add(question);
    }

    public List<Question> getQuestions() {
        return questions;
    }
}

// Main class for user interaction and quiz functionality
public class QuizApp {
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        Quiz quiz = new Quiz();
        initializeQuestions(quiz);

        int score = 0;
        for (Question question : quiz.getQuestions()) {
            displayQuestion(question);
            int userAnswer = getUserAnswer(question);
            if (question.isCorrect(userAnswer)) {
                score++;
            }
        }

        displayScore(score, quiz.getQuestions().size());
    }

    private static void initializeQuestions(Quiz quiz) {
        String[] options1 = {"Java", "Python", "C++", "Ruby"};
        Question q1 = new Question("Which programming language is this quiz written in?", options1, 0);

        String[] options2 = {"OOP", "Procedural", "Functional", "Logic"};
        Question q2 = new Question("What type of programming paradigm does Java follow?", options2, 0);

        quiz.addQuestion(q1);
        quiz.addQuestion(q2);
    }

    private static void displayQuestion(Question question) {
        System.out.println(question.getQuestionText());
        String[] options = question.getOptions();
        for (int i = 0; i < options.length; i++) {
            System.out.println((i + 1) + ". " + options[i]);
        }
    }

    private static int getUserAnswer(Question question) {
        int userAnswer = -1;
        while (true) {
            System.out.print("Enter your answer (1-" + question.getOptions().length + "): ");
            try {
                userAnswer = Integer.parseInt(scanner.nextLine());
                if (userAnswer >= 1 && userAnswer <= question.getOptions().length) {
                    break;
                } else {
                    System.out.println("Invalid option. Please try again.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
        return userAnswer - 1; // Convert to zero-based index
    }

    private static void displayScore(int score, int totalQuestions) {
        System.out.println("Quiz finished!");
        System.out.println("Your score: " + score + "/" + totalQuestions);
    }
}
