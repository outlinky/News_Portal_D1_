## Команды

**1: Создать двух пользователей (с помощью метода User.objects.create_user('username')).**
```
u1 = User.objects.create_user(username='Ivan')
u2 = User.objects.create_user(username='Andrey') 
```

**2: Создать два объекта модели Author, связанные с пользователями.**
```
Author.objects.create(authorUser=u1)
Author.objects.create(authorUser=u2) 
```

**3: Добавить 4 категории в модель Category.**
```
Category.objects.create(name='IT')
Category.objects.create(name='Politics') 
Category.objects.create(name='World')    
Category.objects.create(name='Economy') 
```

**4: Добавить 2 статьи и 1 новость.**
```
author = Author.objects.get(id=1)
author
Post.objects.create(author=author, categoryType='NW', title='sometitle', text='somebigtext')
author2 = Author.objects.get(id=2)
Post.objects.create(author=author, categoryType='AR', title='sometitleofArcticle', text='somebigArticle')
Post.objects.create(author=author2, categoryType='AR', title='sometitleofArcticle2', text='somebigArticle2')
```

**5: Присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий).**
```
Post.objects.get(id=1).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=1).postCategory.add(Category.objects.get(id=2)) 
Post.objects.get(id=2).postCategory.add(Category.objects.get(id=3))                                          
Post.objects.get(id=2).postCategory.add(Category.objects.get(id=4)) 
Post.objects.get(id=3).postCategory.add(Category.objects.get(id=1)) 
Post.objects.get(id=3).postCategory.add(Category.objects.get(id=4))
```

**6: Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий).**
```
Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=1).authorUser, text='anytextbyauthor')
Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=2).authorUser, text='very well comment') 
Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=2).authorUser, text='very bad comment')  
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=1).authorUser, text='very neutral comment') 
```

**7: Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов.**
```
Comment.objects.get(id=1).like()
Comment.objects.get(id=1).rating
Comment.objects.get(id=2).like() 
Comment.objects.get(id=2).like()
Comment.objects.get(id=2).rating 
Comment.objects.get(id=3).dislike() 
Comment.objects.get(id=3).rating    
Post.objects.get(id=1).dislike()    
Post.objects.get(id=1).rating   
Post.objects.get(id=2).dislike() 
Post.objects.get(id=2).rating 
Post.objects.get(id=3).like()    
Post.objects.get(id=3).like()
Post.objects.get(id=3).rating
```

**8: Обновить рейтинги пользователей.**
```
a = Author.objects.get(id=1) 
a.update_rating()
a.ratingAuthor
a2 = Author.objects.get(id=2) 
a2.update_rating()
a2.ratingAuthor
```

**9: Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта).**
```
best_user = Author.objects.order_by('-ratingAuthor')[:1]
for i in best_user:                          
     i.ratingAuthor
     i.authorUser.username
```

**10: Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье.**
```
best_post = Post.objects.all().order_by('-rating')[0]  
best_post.dateCreation.strftime('%Y-%m-%d') 
best_post.author.authorUser.username  
best_post.title
best_post.preview()
```

**11: Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье.**
```
best_comments = best_post.comment_set.all()

for c in best_comments:
    print(c.dateCreation.strftime('%Y-%m-%d'))
    print(c.commentUser)
    print(c.rating)
    print(c.text)
    print()
```
