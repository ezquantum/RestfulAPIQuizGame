import os
from flask import Flask, request, abort, jsonify
from flask_sqlalchemy import SQLAlchemy
from flask_cors import CORS
import random

from models import setup_db, Question, Category

QUESTIONS_PER_PAGE = 10

def paginator(request, selection):
    page = request.args.get('page', 1, type=int)
    start = (page - 1) * QUESTIONS_PER_PAGE
    end = start + QUESTIONS_PER_PAGE
    questions = [question.format() for question in selection]
    current_questions = questions[start:end]
    return current_questions

def create_app(test_config=None):
    app = Flask(__name__)
    setup_db(app)
    # if self.app is not None:
    #     return self.app
    
    # set up CORS, allowing all origins
    CORS(app, resources={'/': {'origins': '*'}})

    @app.after_request
    def after_request(response):
        '''
        Sets access control.
        '''
        response.headers.add('Access-Control-Allow-Headers',
                             'Content-Type,Authorization,true')
        response.headers.add('Access-Control-Allow-Methods',
                             'GET,PUT,POST,DELETE,OPTIONS')
        return response

    @app.route('/')
    def index():
        return 'This is the secret home page'

    @app.route('/categories')
    def categories_get():
        try:
            categories = Category.query.all()
            category_kvp = {}
            for category in categories:
                category_kvp[category.id] = category.type

            return jsonify({
                'success': True,
                'categories': category_kvp
            }), 200

        except:
            abort(500)

    # '''
    # @TODO: 
    # Create an endpoint to handle GET requests 
    # for all available categories.
    # '''
    # ###CHECKU

    ###dafuq

    """Paginates questions and returns categories"""
    @app.route('/questions')
    def get_questions():
        '''
        Handles GET requests for getting all questions.
        '''

        # get all questions and paginate
        selection = Question.query.all()
        total_questions = len(selection)
        current_questions = paginator(request, selection)

        # get all categories and add to dict
        categories = Category.query.all()
        categories_dict = {}
        for category in categories:
            categories_dict[category.id] = category.type

        # abort 404 if no questions
        if (len(current_questions) == 0):
            abort(404)

        # return data to view
        return jsonify({
            'success': True,
            'questions': current_questions,
            'total_questions': total_questions,
            'categories': categories_dict
        })
    # '''
    # @TODO: 
    # Create an endpoint to handle GET requests for questions, 
    # including pagination (every 10 questions). 
    # This endpoint should return a list of questions, 
    # number of total questions, current category, categories. 

    # TEST: At this point, when you start the application
    # you should see questions and categories generated,
    # ten questions per page and pagination at the bottom of the screen for three pages.
    # Clicking on the page numbers should update the questions. 
    # '''


    @app.route('/questions/<int:id>', methods=['DELETE'])
    def del_question(id):

        try:
            question = Question.query.get(id)
            question.delete()

            return jsonify({
                'success': True,
                'message': "The question has been taken to a Black site"
            }), 200
        except:
            abort(422)

    # '''
    # @TODO: 
    # Create an endpoint to DELETE question using a question ID. 

    # TEST: When you click the trash icon next to a question, the question will be removed.
    # This removal will persist in the database and when you refresh the page. 
    # '''

    @app.route('/questions', methods=['POST'])
    def create_question():

        data = request.get_json()

        submission=request.get_json()

        answer = data.get('answer', '')
        question = data.get('question', '')
        category = data.get('category', '')
        difficulty = data.get('difficulty', '')

        while ((answer=='') or (difficulty=='') or (category=='') or (question=='')):
            abort(422)

        try:
            question = Question(
                answer=answer,
                question=question,
                category=category,
                difficulty=difficulty
            )

            question.insert()

            return jsonify({
                'success': True,
                'message': 'Question accepted'
            }), 201
        except:
            abort(422)

    # '''
    # @TODO: 
    # Create an endpoint to POST a new question, 
    # which will require the question and answer text, 
    # category, and difficulty score.

    # TEST: When you submit a question on the "Add" tab, 
    # the form will clear and the question will appear at the end of the last page
    # of the questions list in the "List" tab.  
    # '''

    @app.route('/questions/search', methods=['POST'])
    def search_questions():

        data=request.get_json()
        search_input=data.get('searchTerm', '')

        while search_input =='':
            abort(422)

        try:
            questions = Question.query.filter(
                Question.question.ilike(f'%{search_input}%'.all())
            )

            if len(questions) ==0:
                abort(404)

            questions = Question.query.filter_by(category=id).all()
            paginated_questions = paginator (request, questions)

            return jsonify({
                'success':True,
                'questions': paginated_questions,
                'total_questions': len(Question.query.all())
            }), 200

        except:
            abort(404)
            
    # '''
    # @TODO: 
    # Create a POST endpoint to get questions based on a search term. 
    # It should return any questions for whom the search term 
    # is a substring of the question. 

    # TEST: Search by any phrase. The questions list will update to include 
    # only question that include that string within their question. 
    # Try using the word "title" to start. 
    # '''

    @app.route('/categories/<int:id>/questions')
    def return_question_by_category(id):

        category = Category.query.filter_by(id=id).one_or_none()
        

        if (category is None):
            abort(422)

        questions = Question.query.filter_by(category=id).all()
        paginated_questions = paginator(
        request, questions)
        
        return jsonify({
            'success': True,
            'questions': paginated_questions,
            'total_questions': len(questions),
            'current_category': category.type
        })

    # '''
    # @TODO: 
    # Create a GET endpoint to get questions based on category. 

    # TEST: In the "List" tab / main screen, clicking on one of the 
    # categories in the left column will cause only questions of that 
    # category to be shown. 
    # '''

    @app.route('/quizzes', methods=['POST'])
    def play_quiz():
        data = request.get_json()
        old_questions = data.get('previous_questions')
        quiz_category = data.get('quiz_category')

        if ((quiz_category is None) or (old_questions is None)):
            print(old_questions)
            abort(400)

        if (quiz_category['id'] ==0):
            questions = Question.query.all()
        else:
            questions = Question.query.filter_by(category=quiz_category['id']).all()
            
        def get_random_question():
            return questions[random.randint(0, len(questions)-1)]
        next_question = get_random_question()
        
        available = True
        while available:
            if next_question.id in old_questions:
                next_question = get_random_question()
            else:
                available = False

        return jsonify({
            'success':True,
            'question': next_question.format()
        }), 200

    # '''
    # @TODO: 
    # Create a POST endpoint to get questions to play the quiz. 
    # This endpoint should take category and previous question parameters 
    # and return a random questions within the given category, 
    # if provided, and that is not one of the previous questions. 

    # TEST: In the "Play" tab, after a user selects "All" or a category,
    # one question at a time is displayed, the user is allowed to answer
    # and shown whether they were correct or not. 
    # '''

    @app.errorhandler(400)
    def bad_question(error):
        return jsonify({
            'success': False, 
            'error': 400,
            'message': 'https://httpstatusdogs.com/400-bad-request'
        }), 400

    @app.errorhandler(404)
    def not_found(error):
        return jsonify({
            'success': False,
            'error': 404,
            'message': 'Resource not found'
        }), 404

    @app.errorhandler(500)
    def internal_server_error(error):
        return jsonify({
            'success': False,
            'error': 500,
            'message': 'An error has occured, please try again'
        }), 500

    @app.errorhandler(422)
    def unprocesable_entity(error):
        return jsonify({
            'success': False,
            'error': 422,
            'message': 'Unprocessable entity'
        }), 422

    
    
    return app


    # '''
    # @TODO: 
    # Create error handlers for all expected errors 
    # including 404 and 422. 
    # '''


    