# 233303030425_Marcello_Mac_-TI_4_Malam_A
from django.db import models

class User(models.Model):
    username = models.CharField(max_length=100)
    email = models.EmailField()

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    full_name = models.CharField(max_length=200)

class WasteType(models.Model):
    name = models.CharField(max_length=100)

class Transaction(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    waste_type = models.ForeignKey(WasteType, on_delete=models.CASCADE)
    weight = models.FloatField()
    date = models.DateTimeField(auto_now_add=True)

class Recycler(models.Model):
    name = models.CharField(max_length=100)
    waste_types = models.ManyToManyField(WasteType)



    from rest_framework import serializers
from .models import User, Profile, WasteType, Transaction, Recycler

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = '__all__'

class ProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = Profile
        fields = '__all__'

class WasteTypeSerializer(serializers.ModelSerializer):
    class Meta:
        model = WasteType
        fields = '__all__'

class TransactionSerializer(serializers.ModelSerializer):
    class Meta:
        model = Transaction
        fields = '__all__'

class RecyclerSerializer(serializers.ModelSerializer):
    class Meta:
        model = Recycler
        fields = '__all__'


        from rest_framework import viewsets
from .models import User, Profile, WasteType, Transaction, Recycler
from .serializers import UserSerializer, ProfileSerializer, WasteTypeSerializer, TransactionSerializer, RecyclerSerializer

class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer

class ProfileViewSet(viewsets.ModelViewSet):
    queryset = Profile.objects.all()
    serializer_class = ProfileSerializer

class WasteTypeViewSet(viewsets.ModelViewSet):
    queryset = WasteType.objects.all()
    serializer_class = WasteTypeSerializer

class TransactionViewSet(viewsets.ModelViewSet):
    queryset = Transaction.objects.all()
    serializer_class = TransactionSerializer

class RecyclerViewSet(viewsets.ModelViewSet):
    queryset = Recycler.objects.all()
    serializer_class = RecyclerSerializer



    from django.contrib import admin
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from api import views

router = DefaultRouter()
router.register(r'users', views.UserViewSet)
router.register(r'profiles', views.ProfileViewSet)
router.register(r'waste_types', views.WasteTypeViewSet)
router.register(r'transactions', views.TransactionViewSet)
router.register(r'recyclers', views.RecyclerViewSet)

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include(router.urls)),
]



{
  "username": "Marcello_mac_UPDATED",
  "email": "Marcello_mac_UPDATED@GMAIL.COM"
}


{
  "username": "Marcello_mac",
  "email": "MarcelloMac@GMAIL.COM"
}
